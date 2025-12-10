<template>
  <div class="pdp-container">
    <div class="pdp-grid" v-if="productExists">
      
      <div class="pdp-left">
         <div class="breadcrumb">Best Pets > Electronics > {{ product.name }}</div>
         <div class="hero-image-wrapper">
            <img :src="product.image" class="hero-image" />
         </div>
      </div>

      <div class="pdp-right">
         <h1 class="pdp-title">{{ product.name }}</h1>
         <div class="pdp-meta">
            <span class="model">Model: {{ product.id }}</span>
            <span class="sku">SKU: {{ product.id }}999</span>
         </div>
         <div class="pdp-rating-lg">
             ⭐⭐⭐⭐☆ (4.5) <span class="review-link">See all customer reviews</span>
         </div>
         
         <div class="price-box">
             <div class="main-price">${{ product.price }}</div>
             <div class="price-guarantee">Price Match Guarantee</div>
         </div>

         <div class="fulfillment-box">
             <div class="fulfill-option selected">
                 <div class="radio-circle"></div>
                 <div>
                     <strong>Pickup</strong>
                     <p class="small-text">Ready in 1 hour at Ottawa</p>
                 </div>
             </div>
             <div class="fulfill-option">
                 <div class="radio-circle-empty"></div>
                 <div>
                     <strong>Shipping</strong>
                     <p class="small-text">Free shipping to K1A 0B1</p>
                 </div>
             </div>
         </div>

         <div class="atc-section">
            <button class="pdp-add-btn" @click="addToCart">Add to Cart</button>
         </div>
         
         <div class="pdp-desc">
            <h3>Overview</h3>
            <p>{{ product.description }}</p>
         </div>
      </div>

    </div>
    <div v-else>Loading...</div>
  </div>
</template>

<script>
export default {
  name: 'ProductDetail',
  props: ['products'],
  data() { return { quantity: 1 } },
  computed: {
    product() { return this.products.find(p => p.id == this.$route.params.id); },
    productExists() { return !!this.product; }
  },
  methods: {
    addToCart() {
      this.$emit('addToCart', { productId: this.product.id, quantity: this.quantity })
    }
  }
}
</script>

<style scoped>
.pdp-container {
    background: white;
    padding: 30px;
    border-radius: 8px;
    box-shadow: 0 1px 2px rgba(0,0,0,0.05);
}

.pdp-grid {
    display: grid;
    grid-template-columns: 60% 35%;
    gap: 5%;
}

/* LEFT SIDE */
.breadcrumb { font-size: 12px; color: #555; margin-bottom: 20px; }
.hero-image-wrapper {
    border: 1px solid #e0e6ef;
    padding: 40px;
    border-radius: 4px;
    text-align: center;
}
.hero-image { max-width: 100%; height: auto; }

/* RIGHT SIDE */
.pdp-title { margin-top: 0; font-size: 24px; color: #1d252c; font-weight: 700; }
.pdp-meta { font-size: 11px; color: #555; margin-bottom: 10px; display: flex; gap: 15px; }
.pdp-rating-lg { color: #ffe000; font-size: 14px; margin-bottom: 20px; }
.review-link { color: #0046be; margin-left: 10px; cursor: pointer; }

.price-box { margin-bottom: 25px; }
.main-price { font-size: 32px; font-weight: 800; color: #1d252c; }
.price-guarantee { font-size: 12px; font-weight: 700; color: #1d252c; display: flex; align-items: center; margin-top: 5px; }

.fulfillment-box { border: 1px solid #c5cbd5; border-radius: 4px; margin-bottom: 20px; }
.fulfill-option {
    padding: 15px;
    display: flex;
    gap: 12px;
    border-bottom: 1px solid #e0e6ef;
    cursor: pointer;
}
.fulfill-option:last-child { border-bottom: none; }
.fulfill-option.selected { background-color: #f0f2f4; border-left: 6px solid #0046be; }

.radio-circle { width: 18px; height: 18px; border-radius: 50%; background: #0046be; border: 2px solid #0046be; }
.radio-circle-empty { width: 18px; height: 18px; border-radius: 50%; border: 2px solid #777; }

.small-text { font-size: 12px; margin: 2px 0 0 0; color: #555; }

.pdp-add-btn {
    background-color: #ffce00;
    width: 100%;
    padding: 16px;
    font-size: 18px;
    font-weight: 700;
    border: none;
    border-radius: 4px;
}
.pdp-add-btn:hover { background-color: #ffd933; }

.pdp-desc { margin-top: 30px; border-top: 1px solid #eee; padding-top: 20px; }
</style>