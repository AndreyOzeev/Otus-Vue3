<script setup>
import { ref } from 'vue'
const emit = defineEmits(['search']);
const query = ref('');
const price = ref(null);

function submit() {
  emit('search', { query: query.value, price: price.value })
}
</script>

<template>
  <form class="search-form" @submit.prevent="submit">
    <input v-model="query" placeholder="Поиск по названию..." />
    <input v-model.number="price" placeholder="Цена до" type="number" min="0"/>
    <button type="submit">Найти</button>
  </form>
</template>

<style scoped>
.search-form {
  display: flex;
  gap: 12px;
  justify-content: center;
  margin-bottom: 18px;
}
.search-form input { padding: 6px; }
.search-form button { padding: 7px 15px; }
</style>