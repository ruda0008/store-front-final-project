<template>
  <div class="container">
    <div class="product-detail-container" v-if="productExists">
      
      <div class="detail-left">
        <div class="main-image">
           <img :src="product.image" :alt="product.name" />
        </div>
      </div>

      <div class="detail-right">
        <h1 class="product-name">{{ product.name }}</h1>
        <div class="model-sku">
           <span>Model: {{ product.id }}</span>
           <span>SKU: {{ product.id }}</span>
        </div>
        
        <div class="rating-stars">⭐⭐⭐⭐☆ (4.5)</div>
        
        <hr class="divider">

        <div class="price-block">
          <span class="currency">$</span>
          <span class="amount">{{ product.price }}</span>
        </div>

        <div class="action-box">
          <div class="qty-selector">
             <label>Qty:</label>
             <input type="number" v-model="quantity" min="1" class="qty-input" />
          </div>
          <button class="add-to-cart-lg" @click="addToCart">
            Add to Cart
          </button>
        </div>

        <div class="description-block">
          <h3>Overview</h3>
          <p>{{ product.description }}</p>
        </div>
      </div>
    </div>

    <div class="not-found" v-else>
      <img src="../assets/404.jpg" alt="Product not found" />
      <h3>Oops! That product was not found...</h3>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductDetail',
  props: ['products'],
  data() {
    return {
      quantity: 1
    }
  },
  computed: {
    product() {
      return this.products.find(product => product.id == this.$route.params.id);
    },
    productExists() {
      return !!this.product;
    }
  },
  methods: {
    addToCart() {
      this.$emit('addToCart', {
        productId: this.product.id,
        quantity: this.quantity
      })
    }
  }
}
</script>

<style scoped>
.container {
  background-color: #fff;
  padding: 2rem;
  border-radius: 4px;
}

.product-detail-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  text-align: left;
}

.detail-left img {
  width: 100%;
  border: 1px solid #eee;
  padding: 1rem;
}

.product-name {
  font-size: 1.8rem;
  margin-top: 0;
  margin-bottom: 0.5rem;
}

.model-sku {
  font-size: 0.8rem;
  color: #555;
  margin-bottom: 0.5rem;
}
.model-sku span {
  margin-right: 15px;
}

.rating-stars {
  color: #ffce00;
  margin-bottom: 1rem;
}

.divider {
  border: 0;
  border-top: 1px solid #ccc;
  margin: 1rem 0;
}

.price-block {
  font-size: 2rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
}

.currency {
  font-size: 1rem;
  vertical-align: top;
}

.action-box {
  background-color: #f9f9f9;
  padding: 1.5rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  width: 100%;
  max-width: 300px;
}

.qty-input {
  padding: 5px;
  width: 50px;
  font-size: 1rem;
}

.add-to-cart-lg {
  background-color: #ffce00;
  color: #000;
  border: none;
  padding: 15px;
  font-size: 1.1rem;
  font-weight: bold;
  border-radius: 4px;
  width: 100%;
  cursor: pointer;
}

.add-to-cart-lg:hover {
  background-color: #ffd933;
}

.description-block {
  margin-top: 2rem;
}

@media (max-width: 768px) {
  .product-detail-container {
    grid-template-columns: 1fr;
  }
  .action-box {
    max-width: 100%;
  }
}
</style>