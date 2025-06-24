<template>
  <div class="product-card">
    <img class="product-card__image" :src="product.image" :alt="product.title" height="120" />
    <h2 class="product-card__title">{{ product.title }}</h2>
    <p class="product-card__price">{{ product.price }} $</p>
    <p class="product-card__category">{{ product.category }}</p>
    <p class="product-card__description">{{ product.description }}</p>
  </div>
</template>

<script setup>
defineProps({
  product: { type: Object, required: true }
});
</script>

<style scoped>

.product-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 16px;
  min-height: 400px;

  text-align: center;

  border: 1px solid #dddddd;
  border-radius: 10px;
  box-shadow: 0 2px 8px #dddddd;
  background: #ffffff;

  transition: box-shadow .2s;
}
.product-card:hover {
  box-shadow: 0 4px 16px #dddddd;
}
.product-card__image {
  width: 100px;
  margin-bottom: 12px;
  max-height: 120px;

  border-radius: 5px;

  object-fit: contain;
}
.product-card__title {
  margin-top: 0;
  margin-bottom: 8px;

  font-size: 18px;
}
.product-card__price {
  margin-top: 0;
  margin-bottom: 6px;

  font-weight: bold;

  color: #1976d2;
}
.product-card__category {
  margin-top: 0;
  margin-bottom: 8px;

  font-size: 14px;
  color: #888888;
}
.product-card__description {
  margin-top: 0;
  margin-bottom: 0;

  font-size: 16px;
  color: #444444;
}
</style>