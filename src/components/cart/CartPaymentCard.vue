<template>
  <div class="cart-total">
    <h3>Cart Total: {{ cart_total.toFixed(2) }}</h3>
    <button class="add-basket-button" @click="sendOrder(); $emit('add-basket', product)">Complete</button>
    <div class="stock-error" v-if="err">
      <p>Message: <br> <span>Diş Fırçası is {{ err }}</span> </p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: ["error"],
  data() {
    return {
      err: this.error,
    };
  },
  methods: {
    clearCart() {
      this.$store.commit("clearCart", this.product);
    },
    async sendOrder() {
      const orderData = this.$store.state.cart;
      try {
        const response = await axios.post(
          "https://nonchalant-fang.glitch.me/order",
          orderData
        );
        if (response.data.status === "success") {
          this.clearCart();
        }
      } catch (error) {
        this.err = error.response.data.message;
      }
    },
  },
  computed: {
    cart_total() {
      return this.$store.getters.cartTotal;
    },
  },
};
</script>

<style lang="scss">
.cart-total {
  background-color: #fff;
  padding: 20px;
  .stock-error {
    margin-top: 15px;
    border: 1px solid rgb(255, 0, 42);
    border-radius: .25rem;
    background-color: rgba(255, 0, 42, .9);
    color: #fff;
    p {
      font-size: 18px;
        font-weight: 600;
      span {
        font-size: 15px;
        font-weight: 400;
      }
    }
  }
}
</style>
