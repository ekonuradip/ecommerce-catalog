<template>
  <div class="main-container" :style="{ backgroundColor: isMenCategory ? '#d6e6ff' : '#fde2ff' }">
 
    <div class="content-card">
     
      <div class="left-section">
        <img v-if="product.image" :src="product.image" alt="Foto Produk" />
      </div>

      
      <div class="right-section">
        <h2 :class="{ title: true, women: !isMenCategory }">{{ product.title }}</h2>
        <p>{{ product.category }}</p>
        <div class="rating">
         
        </div>
        <div class="row"></div>
        <div class="category-rating row">
          <p class="category">{{ product.category }}</p>
         
        </div>
        <div class="row"></div> 
        <p class="description">{{ product.description }}</p>
        <div class="row"></div> 
        <p :class="{ price: true, women: !isMenCategory }">Harga: {{ product.price }}</p>
        <div class="buttons">
          <button @click="buyProduct" :class="{ 'button-men': isMenCategory, 'button-women': !isMenCategory }">Buy Product</button>
          <button @click="nextProduct" :class="{ 'button-men2': isMenCategory, 'button-women2': !isMenCategory }">Next Product</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'ProductCard',
  data() {
    return {
      product: {
        title: '',
        category: '',
        description: '',
        price: '',
        image: '',
      },
      currentProductIndex: 1,
    };
  },
  computed: {
    isMenCategory() {
      return this.product.category.toLowerCase() === "men's clothing";
    },
  },
  methods: {
    async fetchProduct() {
      try {
        const response = await axios.get(`https://fakestoreapi.com/products/${this.currentProductIndex}`);
        this.product = response.data;
      } catch (error) {
        console.error('Error fetching product:', error);
      }
    },
    buyProduct() {
      
      console.log('Buy Product clicked');
    },
    nextProduct() {
   
      this.currentProductIndex = this.currentProductIndex === 20 ? 1 : this.currentProductIndex + 1;
      
      this.fetchProduct();
    },
  },
  mounted() {
    this.fetchProduct();
  },
};
</script>

<style scoped>
.main-container {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  margin: 0;
  padding: 0;
}

.content-card {
  background-color: white;
  height: 70%;
  width: 60%;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.5);
  display: flex; 
  align-items: center; 
}

.left-section {
  flex: 1;
  margin-right: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.left-section img {
  max-width: 100%;
  max-height: 200px;
  width: auto;
}

.right-section {
  flex: 2;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

.title {
  font-size: 1.5rem;
  font-weight: bold;
  color: #002772;
  margin-bottom: 10px;
}

.title.women {
  color: #720060; 
}

.row {
  border-bottom: 1px solid #ccc;
  padding: 10px 0;
}

.description {
  margin: 10px 0;
  text-align: left; 
}

.category-rating {
  text-align: left; 
}

.price {
  font-size: 1.5rem;
  font-weight: bold;
  margin: 10px 0;
  text-align: left; 
}

.price.women {
  color: #720060; 
}

.buttons {
  margin-top: 20px;
  text-align: left; 
  display: flex; 
  justify-content: space-between; 
}

button {
  flex: 1; 
  padding: 10px;
  border: none;
  cursor: pointer;
  border-radius: 5px;
  margin-right: 10px; 
}

.button-men {
  background-color: #002772; 
  color: white;
}
.button-men2 {
  background-color: white;
  border: 2px solid #002772; 
  color: #002772;
}

.button-women {
  background-color: #720060; 
  color: white;
}
.button-women2 {
  background-color: white;
  border: 2px solid #720060; 
  color: #720060;
}


</style>
