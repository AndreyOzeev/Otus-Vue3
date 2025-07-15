<template>
  <main class="main">
    <SearchHeader @search="onSearch"/>
    <h1 class="title">Список товаров</h1>
    <div v-if="loading">
      <div class="loader"></div>
    </div>
    <div v-else-if="error">
      <div class="error-block">
        <strong>Ошибка загрузки!</strong>
        <div>{{ error }}</div>
        <button class="error-block__button" @click="reload">Попробовать снова</button>
      </div>
    </div>
    <div v-else>
      <ProductList :products="filteredProducts"/>
    </div>
  </main>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';
import ProductList from './components/ProductList.vue';
import SearchHeader from "./components/SearchHeader.vue";

const error = ref(null);
const products = ref([]);
const loading = ref(true);
const apiUrl = 'https://fakestoreapi.com/products';

const filter = ref({ query: '', price: null });

function onSearch(payload) {
  filter.value = payload;
}

const filteredProducts = computed(() => {
  if ((!filter.value.query || filter.value.query.trim() === '') && (filter.value.price === null || filter.value.price === '')) {
    return products.value;
  }
  return products.value.filter(product => {
    const matchTitle = filter.value.query
        ? product.title.toLowerCase().includes(filter.value.query.toLowerCase())
        : false;
    const matchPrice = filter.value.price !== null && filter.value.price !== ''
        ? product.price <= filter.value.price
        : false;
    return matchTitle || matchPrice;
  });
});

const fetchData = async () => {
  loading.value = true;
  error.value = null;
  try {
    const res = await fetch(apiUrl);
    if (!res.ok) throw new Error('Ошибка сети: ' + res.status);
    products.value = await res.json();
  } catch (err) {
    error.value = err.message;
  } finally {
    loading.value = false;
  }
};

function reload() {
  fetchData();
}

onMounted(fetchData);
</script>

<style scoped>
.main {
  max-width: 1000px;
  margin: 24px auto;
  padding: 12px;
}

.title {
  text-align: center;
}

.loader {
  width: 40px;
  height: 40px;
  margin: 24px auto;
  border: 6px solid #eeeeee;
  border-top: 6px solid #1976d2;
  border-radius: 50%;
  animation: loader-spin 1s linear infinite;
}

@keyframes loader-spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.error-block {
  padding: 20px;
  margin: 30px 0;

  text-align: center;
  color: #af1d1d;

  border: 1px solid #e57373;
  border-radius: 8px;
  background-color: #ffeaea;
}

.error-block__button {
  margin-top: 10px;
  padding: 7px 16px;

  color: #af1d1d;
  border: 1px solid #af1d1d;
  border-radius: 4px;
  background-color: #ffffff;
  cursor: pointer;
  transition: background .2s;
}

.error-block__button:hover {
  background-color: #ffdddd;
}
</style>