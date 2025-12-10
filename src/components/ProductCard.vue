<template>
  <div class="bby-card">
    <div class="bby-card-img">
       <router-link :to="`/product/${product.id}`">
         <img :src="product.image" alt="Product">
       </router-link>
    </div>
    
    <div class="bby-card-body">
      <router-link :to="`/product/${product.id}`" class="bby-title">
        {{ product.name }}
      </router-link>

      <div class="bby-rating">
        <span class="stars">★★★★☆</span>
        <span class="count">(42)</span>
      </div>
      
      <div class="bby-price-block">
        <div class="current-price">${{ product.price }}</div>
        <div class="fulfillment">
           <span class="check">✔</span> Ready in 1 hour
        </div>
      </div>

      <button class="bby-add-btn" @click="addToCart">
        <span class="icon">🛒</span> Add to Cart
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props: ['product'],
  methods: {
    addToCart() {
      this.$emit('addToCart', { productId: this.product.id, quantity: 1 })
    }
  }
}
</script>

<style scoped>
.bby-card {
  background: white;
  border: 1px solid #e0e6ef;
  border-radius: 4px;
  padding: 16px;
  display: flex;
  flex-direction: column;
  height: 100%;
  transition: box-shadow 0.2s;
}

.bby-card:hover {
  box-shadow: 0 4px 14px rgba(0,0,0,0.1);
}

.bby-card-img {
  height: 180px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 12px;
}

.bby-card-img img {
  max-height: 150px;
  max-width: 100%;
  object-fit: contain;
}

.bby-title {
  color: #0046be;
  font-weight: 600;
  font-size: 15px;
  line-height: 1.4;
  text-decoration: none;
  margin-bottom: 8px;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.bby-title:hover {
  text-decoration: underline;
  color: #001e73;
}

.bby-rating {
  font-size: 12px;
  color: #0046be;
  margin-bottom: 12px;
}
.stars { color: #ffe000; text-shadow: 0 0 1px #e6a400; font-size: 14px; }
.count { margin-left: 4px; color: #555; }

.bby-price-block {
  margin-top: auto;
  margin-bottom: 16px;
}

.current-price {
  font-size: 22px;
  font-weight: 700;
  color: #1d252c;
}

.fulfillment {
    font-size: 12px;
    color: #318000;
    margin-top: 4px;
    font-weight: 600;
}

.bby-add-btn {
  background-color: #ffce00;
  border: none;
  border-radius: 4px;
  color: #000;
  font-weight: 700;
  padding: 10px;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  font-size: 14px;
}
.bby-add-btn:hover {
    background-color: #ffd933;
}
</style>