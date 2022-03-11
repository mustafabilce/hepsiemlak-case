<template>
  <div class="cards">
    <div class="cart-item-card">
      <div class="header">
        <img :src="product.image" alt="" />
        <h3>{{ product.name }}</h3>
        <div class="quantity-box">
          <button @click="removeFromCart()">-</button>
          <span>{{ product.quantity }}</span>
          <button @click="addToCart()">+</button>
        </div>
        <h4>Total Cost: {{ item_cost.toFixed(2) }} {{ product.currency }}</h4>
      </div>
      <p>{{ description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["product"],
  methods: {
    addToCart() {
      this.$store.commit("addToCart", this.product);
    },
    removeFromCart() {
      this.$store.commit("removeFromCart", this.product);
    },
  },
  computed: {
    description() {
      return this.product.description;
    },
    item_cost() {
      return this.product.price * this.product.quantity;
    },
  },
};
</script>

<style lang="scss">
.cards {
  width: 90%;
  margin: auto;
  border-radius: 5px;
  img {
    max-height: 100px;
    max-width: 100px;
  }
  .cart-item-card {
    width: 100%;
    margin-bottom: 10px;
    background-color: #fff;
    padding: 10px;
    text-align: left;
    display: flex;
    align-items: center;
    justify-content: center;

    .header {
      width: 100%;
      display: flex;
      justify-content: space-around;
      align-items: center;
      h3,
      h4 {
        margin: 0;
      }
    }
  }
  .quantity-box {
    display: flex;
    span {
      font-size: 1rem;
      font-weight: 600;
      border: 1px solid rgb(255, 96, 0);
      border-radius: 0.25rem;
      padding: 5px 10px;
    }
    button {
      background-color: rgb(255, 96, 0);
      border: none;
      color: #fff;
      font-size: 1rem;
      border-radius: 0.25rem;
      padding: 0 10px;
      text-align: center;
      margin: 0 5px;
      cursor: pointer;
    }
  }
}
@media (max-width: 768px) {
  .cards {
    width: 100%;
    .cart-item-card {
      padding: 0;
      .header {
        text-align: center;
        padding: 0 10px;
      }
      img {
        padding: 8px;
        max-height: 75px;
        max-width: 75px;
      }
      h3,
      h4 {
        font-size: 13px;
      }
      .card {
        margin-bottom: 15px;
      }
      .quantity-box {
        button {
          padding: 5px;
          line-height: 5px;
          margin: 5px;
          display: flex;
          align-items: center;
        }
        span {
          padding: 0 5px;
        }
      }
    }
  }
}
</style>
