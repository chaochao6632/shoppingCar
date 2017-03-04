<template>
  <div id="app">
    <h1>vue2 vuex 购物车 demo</h1>
    <shop-list></shop-list>
    <shop-cart></shop-cart>
    <shop-info></shop-info>
  </div>
</template>

<script>
  import List from './components/shop/list/List.vue'
  import Cart from './components/shop/cart/Cart.vue'
  import Info from './components/shop/info/Info.vue'
  export default {
    name: 'app',
    data() {
      return {
        msg: 'Welcome to Your Vue.js App'
      }
    },
    components: {
      ShopList: List,
      ShopCart: Cart,
      ShopInfo: Info
    }
  }
</script>

<style lang="scss">
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  
  h1,
  h2 {
    font-weight: normal;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    display: inline-block;
    margin: 0 10px;
  }
  
  a {
    color: #42b983;
  }
</style>