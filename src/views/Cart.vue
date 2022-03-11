<template>
  <div>
    <h1>Your Cart</h1>
    <div class="container">
      <div class="row">
        <div class="col-9">
          <div v-if="$store.state.cart.length >= 1">
            <CartItemCard
              v-for="product in products"
              :key="product.id"
              :product="product"
            />
          </div>
          <div v-else>
            <h1>Order Received!</h1>
            <h3>Your cart is empty.</h3>
            <p>
              <router-link :class="{ active: $route.name === 'Home' }" to="/"
                >Back to shopping.</router-link
              >
            </p>
          </div>
        </div>
        <div class="col-3">
          <CartPaymentCard />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CartItemCard from "../components/cart/CartItemCard.vue";
import CartPaymentCard from "../components/cart/CartPaymentCard.vue";

export default {
  components: {
    CartItemCard,
    CartPaymentCard,
  },
  computed: {
    products() {
      return this.$store.getters.cartItems;
    },
  },
};
</script>

<style lang="scss">
.row {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -ms-flex-wrap: wrap;
  flex-wrap: wrap;
  margin-right: -15px;
  margin-left: -15px;
}
.col-9 {
  -webkit-box-flex: 0;
  -ms-flex: 0 0 75%;
  flex: 0 0 75%;
  max-width: 75%;
}
.col-3 {
  -webkit-box-flex: 0;
  -ms-flex: 0 0 25%;
  flex: 0 0 25%;
  max-width: 25%;
}
@media (max-width: 768px) {
  .row {
    display: block;
    margin: 0;
  }
  .col-9, .col-3 {
    max-width: 100%;
  }
}
</style>
