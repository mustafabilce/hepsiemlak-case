<template>
  <div class="card">
    <img :src="product.image" alt="" />
    <h3>{{ product.name }}</h3>
    <p class="description">{{ product.price }} {{ product.currency }}</p>
    <button class="add-product-button" @click="addToCart(); $emit('add-basket', product)">Add Basket</button>
  </div>
</template>

<script>
export default {
  props: ["product"],
  computed: {
    description() {
      return this.product.description.substring(0, 150);
    },
  },
};
</script>