<template>
  <div class="card">
    <img :src="product.image" alt="" />
    <h3>{{ product.name }}</h3>
    <p class="description">{{ product.price }} {{ product.currency }}</p>
    <button
      class="add-product-button"
      @click="
        addToCart();
        $emit('add-basket', product);
      "
    >
      Add Basket
    </button>
  </div>
</template>

<script>
export default {
  props: ["product"],
  methods: {
    addToCart() {
      this.$store.commit("addToCart", this.product);
      this.$toast.success(`${this.product.name} has been added to the cart.`);
    },
  },
  computed: {
    description() {
      return this.product.description.substring(0, 150);
    },
  },
};
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
  transition: 0.3s;
  &:hover {
    background-color: rgba(255, 96, 0, 0.2);
    color: rgb(255, 96, 0);
  }
}

@media (max-width: 768px) {
  .card {
    margin-bottom: 15px;
  }
}
</style>
