<template>
  <div class="cart-total">
    <h3>Cart Total: {{ cart_total.toFixed(2) }}</h3>
    <button class="add-basket-button" @click="sendOrder(); $emit('add-basket', product)">Complete</button>
  </div>
</template>

<script>
import config from '../../config'
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
    errorNotification() {
      this.$toast.error(`${this.product.name} out of stock.`);
    },
    async sendOrder() {
      const orderData = this.$store.state.cart;
      try {
        const response = await axios.post(
          `${config.apiUrl}/order`,
          orderData
        );
        if (response.data.status === "success") {
          this.clearCart();
          this.$toast.success(`Order Received!`);
        }
      } catch (error) {
        this.err = error.response.data.message;
        this.$toast.error(`Diş Fırçası ${error.response.data.message}`);
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
