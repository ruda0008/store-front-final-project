<template>
  <div class="app-wrapper">
    <TopNav :cartItemCount="cartItemCount"/>
    <div class="main-content">
      <router-view
        :products="products"
        :cartItems="cartItems"
        @addToCart="addToCart"
        @removeFromCart="removeFromCart"
        @submitOrder="submitOrder"
      ></router-view>
    </div>
    <footer class="bby-footer">
      <div class="footer-links">
        <span>Accessibility</span>
        <span>Terms & Conditions</span>
        <span>Privacy Policy</span>
        <span>Interest-Based Ads</span>
      </div>
      <p>© 2025 Best Pets Electronics. All rights reserved.</p>
    </footer>
  </div>
</template>

<script>
import TopNav from './components/TopNav.vue'

export default {
  name: 'App',
  components: {
    TopNav
  },
  data() {
    return {
      cartItems: [],
      products: [],
    }
  },
  computed: {
    cartItemCount() {
      return this.cartItems.reduce((total, item) => {
        return total + item.quantity
      }, 0)
    }
  },
  mounted() {
    this.getProducts()
  },
  methods: {
    getProducts() {
      fetch('/products')
        .then(response => response.json())
        .then(products => {
          this.products = products
        })
        .catch(error => {
          console.error(error)
        })
    },
    addToCart({ productId, quantity }) {
      const existingCartItem = this.cartItems.find(item => item.product.id == productId)
      if (existingCartItem) {
        existingCartItem.quantity += quantity
      } else {
        const product = this.products.find(product => product.id == productId)
        this.cartItems.push({ product, quantity })
      }
    },
    removeFromCart(index) {
      this.cartItems.splice(index, 1)
    },
    submitOrder() {
      const order = {
        customerId: Math.floor(Math.random() * 10000000000).toString(),
        items: this.cartItems.map(item => ({
          productId: item.product.id,
          quantity: item.quantity,
          price: item.product.price
        }))
      }
      fetch(`/order`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(order)
      }).then(response => {
        if (response.ok) {
          this.cartItems = []
          alert('Order submitted successfully')
        } else {
          alert('Error submitting order')
        }
      })
    }
  }
}
</script>

<style>
/* BEST BUY GLOBAL RESET */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap');

body {
  margin: 0;
  padding: 0;
  background-color: #f0f2f4; /* Official Light Gray BG */
  font-family: 'Inter', sans-serif; /* Closest free match to Human BBY */
  -webkit-font-smoothing: antialiased;
  color: #1d252c;
}

.app-wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.main-content {
  flex: 1;
  max-width: 1400px;
  width: 100%;
  margin: 0 auto;
  padding: 24px;
  box-sizing: border-box;
  padding-top: 90px; /* Offset for fixed header */
}

.product-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 16px;
}

.bby-footer {
  background-color: #f0f2f4;
  border-top: 1px solid #dcdcdc;
  padding: 40px 20px;
  text-align: center;
  font-size: 11px;
  color: #555;
}

.footer-links {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin-bottom: 10px;
  color: #0046be;
  font-weight: 600;
}
</style>