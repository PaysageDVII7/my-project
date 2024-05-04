<template>
  <div id="app">
    <TopMenu :cart-items="cartItems" />
    <ProductCard @add-to-cart="handleAddToCart" />
  </div>
</template>

<script>
import TopMenu from './components/TopMenu.vue'
import ProductCard from './components/ProductCard.vue'

export default {
  name: 'App',
  components: {
    TopMenu,
    ProductCard
  },
  data() {
    return {
      cartItems: []  
    };
  },
  methods: {
    handleAddToCart(product) {
      let found = this.cartItems.find(item => item.id === product.id && item.size === product.size);
      if (found) {
        found.quantity += 1;
      } else {
        this.cartItems.push(product);
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>

