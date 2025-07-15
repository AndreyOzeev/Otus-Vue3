<script setup>
import {ref} from 'vue'

const emit = defineEmits(['search']);
const query = ref('');
const price = ref(null);

function submit() {
  emit('search', {query: query.value, price: price.value})
}
</script>

<template>
  <form class="search-form" @submit.prevent="submit">
    <input class="search-form__input" v-model="query" placeholder="Поиск по названию..."/>
    <input class="search-form__input" v-model.number="price" placeholder="Цена до" type="number" min="0"/>
    <button class="search-form__button" type="submit">Найти</button>
  </form>
</template>

<style scoped>
.search-form {
  display: flex;
  gap: 12px;
  justify-content: center;
  margin-bottom: 18px;
}

.search-form__input {
  padding: 6px;
}

.search-form__button {
  padding: 7px 15px;
}
</style>
