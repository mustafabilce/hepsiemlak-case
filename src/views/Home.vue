<template>
  <div class="home">
    <div class="product-card-container">
      <ProductCard
        v-for="product in items"
        :key="product.id"
        :product="product"
        v-on:add-basket="viewProduct($event)"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import ProductCard from "../components/product/ProductCard.vue";

export default {
  name: 'Home',
  components: {
    ProductCard,
  },
  data() {
    return {
      items: [],
      errors: [],
      product: null,
      active: {
        product_notification: false,
      },
    };
  },
  async created() {
    await this.getProducts();
  },
  methods: {
    getProducts() {
      axios
        .get("https://nonchalant-fang.glitch.me/listing")
        .then((response) => (this.items = response.data))
        .catch((error) => {
          this.errors.push(error);
        });
    },
  }
}
</script>
