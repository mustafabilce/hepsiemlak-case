<template>
    <div class="notification-background" :class="{show: active}" @click="$emit('close-product-notification')" />
    <div class="notification" :class="{show: active}">
        <div class="notification-close" @click="$emit('close-product-notification')">
            X
        </div>
        <div v-if="product" class="product-details">
            <p>{{ product.name }} has been added to the cart.</p>
        </div>
    </div>
</template>

<script>
export default {
    props: ['product', 'active'],
    computed: {
        product_total() {
            return this.$store.getters.productQuantity(this.product)
        }
    }
}
</script>

<style lang="scss">
    .notification {
        width: 400px;
        height: 50px;
        background-color: #fff;
        position: absolute;
        top: 10px;
        right: -105vh;
        padding: 15px;
        transition: right .5s;
        z-index: 101;
        overflow-y: scroll;

        &.show {
            right: 10px;
            border-radius: .25rem;
            border: 1px solid #54c942;
        }
    }
    .notification-close {
        font-size: 1rem;
        padding: 5px;
        border-radius: 5px;
        right: 10px;
        color: gray;
        width: 15px;
        float: right;
        cursor: pointer;

        &:hover {
            background-color: lightgray;
        }
    }
    .product-details {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        height: 100%;

        h3 {
            margin-bottom: 5px;
        }

        &.p {
            padding: 20px;
            line-height: 1.5rem;
        }

        .card-total {
            margin-bottom: 15px;
        }

        .button-container {
            button {
                width: 150px;
                border: none;
                padding: 10px;
                border-radius: 5px;
                margin: 0 5px 50px 5px;
                cursor: pointer;
            }
        }
    }
@media (max-width: 768px) {
  .notification {
      width: 200px;
      padding: 10px;
      .notification-close {
          width: 10px;
          font-size: .7rem;
          padding: 0;
      }
      p {
          font-size: 12px;
      }
  }
}
</style>