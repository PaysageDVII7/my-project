<template> 
  <div class="product-cardX"> 
    <div class="product-card" v-if="product"> 
        <div class="product-image">
            <img :src="product.imageURL" alt="Product Image">
        </div>   
        <div class="product-info">
            <h3>{{ product.title }}</h3>
            <p class="price">${{ product.price }}</p>
            <p class="description">{{ product.description }}</p>
            <p class="size-label">SIZE<span style="color: red;">* </span> {{ selectedSizeLabel }}</p>
            <div class="sizes">
                <button v-for="size in product.sizeOptions" :key="size.id"
                        :class="{ 'active': selectedSize === size.id }"
                        @click="selectSize(size)">
                {{ size.label }}
                </button>
            </div>
            <button class="action-button" @click="PreAddtoCart(size)">ADD TO CART</button>
        </div>
    </div>
    <div v-else>
        Loading product...
    </div> 
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'ProductCard',
  data() {
    return {
      product: null,
      selectedSize: null,
      selectedSizeLabel: ''
    }
  },
  created() {
    this.fetchProduct();
  },
  methods: {
    fetchProduct() {
      axios.get('https://3sb655pz3a.execute-api.ap-southeast-2.amazonaws.com/live/product')
        .then(response => {
          this.product = response.data;
        })
        .catch(error => {
          console.error('There was an error fetching the product:', error);
        });
    },
    selectSize(size) {
        if (this.selectedSize === size.id) { 
            this.selectedSize = null;
            this.selectedSizeLabel = '';
        } else { 
            this.selectedSize = size.id;
            this.selectedSizeLabel = size.label;
        }
    }, 
    PreAddtoCart() { 
      if (this.selectedSize == null || this.selectedSizeLabel == ''){
        alert('Please select a size.');
      } else {
        this.addToCart();
      }
    },
    addToCart() {
      this.$emit('add-to-cart', {
        id: this.product.id,
        name: this.product.title,
        price: this.product.price,
        size: this.selectedSizeLabel,
        image: this.product.imageURL,
        quantity: 1
      });
    }
  }
}
</script>

<style scoped>
.product-cardX {  
  width: 60%; 
  margin: 30px auto;  
  padding: 0px 0px 0px 5%;
}

.product-card {
  display: flex;  

} 

@media (max-width: 768px) {
  .product-card {
    flex-direction: column; 
    
  }

  .product-info { 
    margin-top: 40px;
    width: 80%;   
  }
  .product-image {
    margin-left: 0;
    width: 100%;   
  }
  .product-image img {
    width: 100%;   
  }
  .product-cardX {
    width: 100%;  
    margin: 10px 0;  
    padding: 0;  
  }
}
 

.product-image img {
  width: 400px;
  height: auto;
}

.product-info {
  margin-left: 15%;
  text-align: left;   
}

.product-info h3 {
  margin: 0;
  padding-bottom: 20px;
  text-align: left;
  border-bottom: 1px solid #f1f1f1;
  color: #222222;
}

.product-info .price {
  margin: 0;
  font-weight: bold;  /* BOLD */
  font-size: 14px;
  padding-top: 8px;
  padding-bottom: 8px;
  text-align: left;
  border-bottom: 1px solid #f1f1f1;
  color: #222222;
}

.product-info .description {
  margin: 0;
  line-height: 1.6;
  font-size: 13px;
  padding-top: 20px;
  padding-bottom: 10px;
  text-align: left; 
  color: #888888;
}
 
.sizes {
  display: flex; 
  align-items: center;  
}

.size-label{ 
  margin-top: 5%;
  font-size: 11px;  
  font-weight: bold;  /* BOLD */
}

.sizes button {
  background-color: white;
  border: 2px solid #CCCCCC;
  color: #888888;
  text-align: center;
  margin-right: 5px;
  width: 40px;  
  height: 40px;  
  display: flex;
  justify-content: center;  
  align-items: center;  
  cursor: pointer;
  font-size: 11px;  
}

.sizes button.active,
.sizes button:hover {
  border-color: black;
  color: black;
  transition-delay: 200ms;
}

.action-button {
  background-color: white;
  border: 2px solid black;
  color: black;
  padding: 10px 20px;
  cursor: pointer;
  margin-top: 20px;
  width: 140px;
  font-weight: bold;  /* BOLD */
}

.action-button:hover {
  background-color: black;
  color: white;
}
</style>
