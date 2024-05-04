<template>
  <div class="top-menu">
    <div class="menu-content"  @click="toggleCart">
      My Cart ({{ cartItems.length }})
    </div>
    <div v-if="showCart" class="cart-dropdown">
      <div class="cart-item" v-for="item in cartItems" :key="item.id">
        <img :src="item.image" alt="Product" class="cart-item-image">
        <div class="cart-item-details">
          <p>{{ item.name }}</p>
          <p>{{ item.quantity }} × <span style="font-weight: bold;">${{ item.price }}</span></p>
          <p>Size: {{ item.size }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TopMenu',
  data() {
    return {
      showCart: false
    };
  },
  props: {
    cartItems: Array
  },
  methods: {
    toggleCart() {
      if (this.cartItems != null && this.cartItems.length > 0){
        this.showCart = !this.showCart;
      }
    }
  }
}
</script>
 

<style scoped>
.top-menu {
  background-color: #F6F6F7;
  text-align: right;
  padding: 9px 20px;
  width: 83%; 
  margin: 15px auto;
  cursor: pointer;  
  position: relative; 
  
}

.menu-content {
  font-size: 11px;
  color: #888888;
  margin-right: 11%; 
  position: relative; 
}

.cart-dropdown {
  position: absolute;
  right: 0;
  background-color: white;
  margin-top: 9px;
  width: 300px;  
  z-index: 100; 
  border: 1px solid #f1f1f1;
  margin-right: 11%; 
}

.cart-item {
  display: flex;
  align-items: flex-start;
  padding: 10px;
  
}

.cart-item-image { 
  width: 80px; 
  margin-right: 30px;
}

.cart-item-details p {
  margin: 13px 0;
  text-align: left;
  font-size: 13px;
}
</style>