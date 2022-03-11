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
    viewProduct(product) {
      this.product = product;
      this.active.product_notification = true;
    },
  }
}
</script>

<style lang="scss">
.card {
  width: auto;
  padding: 10px;
  border-radius: 5px;
  background-color: #fff;
  border: 1px solid rgba(0, 0, 0, 0.125);

  img {
    max-width: 100px;
  }

  h5.price {
    color: gray;
  }

  p.description {
    font-size: 0.85rem;
  }

  p.text-muted {
    color: gray;
  }
}

button.add-basket-button {
  padding: 10px 20px;
  background-color: rgb(255, 96, 0);
  border: none;
  color: #fff;
  font-weight: bold;
  font-size: 0.8rem;
  border-radius: 0.25rem;
  cursor: pointer;
}

button.add-product-button {
  padding: 10px 20px;
  background-color: rgb(255, 96, 0);
  border: none;
  color: #fff;
  font-weight: bold;
  font-size: 0.8rem;
  border-radius: 0.25rem;
  cursor: pointer;
  margin-left: 10px;
  transition: .3s;
  &:hover {
    background-color: rgba(255, 96, 0, .2);
    color: rgb(255, 96, 0);
  }
}
@media (max-width: 768px) {
  .card {
    margin-bottom: 15px;
  }
}
</style>
