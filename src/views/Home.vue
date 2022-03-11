<template>
  <div class="home">
    <div class="spinner-box" v-if="loading">
       <easy-spinner />
    </div>
    <div v-else>
      <div class="product-card-container">
        <ProductCard
          v-for="product in items"
          :key="product.id"
          :product="product"
        />
      </div>
    </div>
  </div>
</template>

<script>
import config from '../config'
import axios from "axios";
import ProductCard from "../components/product/ProductCard.vue";

export default {
  name: "Home",
  components: {
    ProductCard,
  },
  data() {
    return {
      loading: false,
      items: [],
      errors: [],
      product: null,
    };
  },
  async created() {
    await this.getProducts();
  },
  methods: {
    getProducts() {
      this.loading = true;
      axios
        .get(`${config.apiUrl}/listing`)
        .then((response) => (this.items = response.data))
        .catch((error) => {
          this.errors.push(error);
        })
        .finally(() => (this.loading = false));
    },
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
.spinner-box {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
    svg {
      width: 3em;
      height: 3em;
    }
}
@media (max-width: 768px) {
  .product-card-container {
    display: block;
  }
}
</style>
