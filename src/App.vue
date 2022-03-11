<template>
    <div id="nav">
    <router-link :class="{active: $route.name === 'Home'}" to="/">Home</router-link> |
    <router-link :class="{active: $route.name === 'Cart'}" to="/cart">Cart <span class="product-quantity">{{ $store.state.cart.length }}</span> </router-link>
  </div>
  <router-view/>
</template>

<script>

export default {
}
</script>

<style lang="scss">
@media (min-width: 768px) {
  #app {
    width: 750px;
  }
}
@media (min-width: 992px) {
  #app {
    width: 970px;
  }
}
@media (min-width: 1200px) {
  #app {
    width: 1170px;
  }
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
  overflow-x: hidden;
}
html, body {
  margin: 0;
  padding: 0;
  overflow-x: hidden;
}
body {
  background-color: rgb(245, 245, 245);
}
#nav {
  padding: 10px;
  width: 100%;
  height: 30px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.125);
  line-height: 30px;

  a {
    font-weight: bold;
    color: darkgray;
    text-decoration: none;
    margin: 0 5px 0 5px;
    font-size: 1.25rem;

    &.active {
      color: #2c3e50;
    }
  }
  .product-quantity {
    background-color: rgb(255, 96, 0);
    color: #fff;
    padding: 5px 8px;
    border-radius: 50%;
    font-size: .7rem;
    line-height: .7rem;
  }
}
.text-center {
  text-align: center;
}
</style>
