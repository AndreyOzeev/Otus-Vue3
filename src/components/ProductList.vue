<template>
  <div class="product-grid">
    <ProductItem v-for="item in products"
                 :key="item.id"
                 :product="item" />
  </div>
</template>

<script setup>
import ProductItem from './ProductItem.vue';
defineProps({
  products: { type: Array, required: true }
});
</script>

<style scoped>
.product-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}
</style>