<template>
  <div class="home">
    <div class="product-card-container">
      <ProductCard
        v-for="product in items"
        :key="product.id"
        :product="product"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import ProductCard from "../components/product/ProductCard.vue";

export default {
  name: "Home",
  components: {
    ProductCard,
  },
  async created() {
    await this.getProducts();
  },
  data() {
    return {
      items: [],
      errors: [],
      product: null,
    };
  },
  methods: {
    getProducts() {
      axios
        .get("https://nonchalant-fang.glitch.me/listing")
        .then((response) => (this.items = response.data))
        .catch((error) => {
          this.errors.push(error);
        });
    }
  },
};
</script>

<style lang="scss">
.product-card-container {
  width: 100%;
  margin: 15px 0;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: 1fr;
  grid-column-gap: 15px;
  grid-row-gap: 15px;
}
@media (max-width: 768px) {
  .product-card-container {
    display: block;
  }
}
</style>
