<template>
  <div class="home">
    <Notification
      :product="product"
      :active="active.product_notification"
      v-on:close-product-notification="closeProductNotification()"
    />
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
import Notification from "../components/product/Notification.vue";

export default {
  name: "Home",
  components: {
    ProductCard,
    Notification,
  },
  async created() {
    await this.getProducts();
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
  methods: {
    getProducts() {
      axios
        .get("https://nonchalant-fang.glitch.me/listing")
        .then((response) => (this.items = response.data))
        .catch((error) => {
          this.errors.push(error);
        });
    },
    viewProduct(product) {
      this.product = product;
      this.active.product_notification = true;
    },
    closeProductNotification() {
      this.active.product_notification = false;
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
@media (max-width: 768px) {
  .product-card-container {
    display: block;
  }
}
</style>
