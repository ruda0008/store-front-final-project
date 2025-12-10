<template>
  <div class="product-card">
    <div class="card-image">
      <img :src="product.image" alt="Product Image">
    </div>
    
    <div class="card-content">
      <router-link :to="`/product/${product.id}`" class="product-title">
        {{ product.name }}
      </router-link>
      
      <div class="ratings">⭐⭐⭐⭐☆ (12)</div>

      <div class="price-container">
        <span class="price-symbol">$</span>
        <span class="price-value">{{ product.price }}</span>
      </div>
      
      <div class="product-controls">
        <button class="add-btn" @click="addToCart">
           <span class="cart-icon">🛒</span> Add to Cart
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props: ['product'],
  data() {
    return {
      quantity: 1
    }
  },
  methods: {
    addToCart() {
      // Defaulting to quantity 1 for grid view to simplify UI like BestBuy
      this.$emit('addToCart', {
        productId: this.product.id,
        quantity: 1
      })
    }
  }
}
</script>

<style scoped>
.product-card {
  display: flex;
  flex-direction: column;
  background-color: #fff;
  border: 1px solid #e0e6ef;
  border-radius: 4px;
  padding: 16px;
  transition: box-shadow 0.2s;
  height: 100%;
  box-sizing: border-box;
  text-align: left;
}

.product-card:hover {
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  border-color: #c5cbd5;
}

.card-image {
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 1rem;
}

.card-image img {
  max-height: 100%;
  max-width: 100%;
  object-fit: contain;
}

.product-title {
  font-size: 1rem;
  font-weight: 600;
  color: #0046be; /* Link Blue */
  margin-bottom: 5px;
  display: block;
  line-height: 1.4;
  height: 45px; /* Limit height for uniform cards */
  overflow: hidden;
}

.product-title:hover {
  text-decoration: underline;
}

.ratings {
  font-size: 0.8rem;
  color: #fce803; /* Star color */
  margin-bottom: 10px;
}

.price-container {
  margin-top: auto;
  margin-bottom: 15px;
}

.price-symbol {
  font-size: 0.9rem;
  vertical-align: top;
  font-weight: bold;
}

.price-value {
  font-size: 1.5rem;
  font-weight: 700;
}

.add-btn {
  width: 100%;
  background-color: #ffce00; /* Best Buy Yellow */
  color: #000;
  border: none;
  padding: 10px;
  font-weight: 700;
  border-radius: 4px;
  font-size: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  transition: background-color 0.2s;
}

.add-btn:hover {
  background-color: #ffd933;
}
</style>