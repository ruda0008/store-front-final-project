<template>
  <TopNav :cartItemCount="cartItemCount"/>
  <div class="main-container">
    <router-view
      :products="products"
      :cartItems="cartItems"
      @addToCart="addToCart"
      @removeFromCart="removeFromCart"
      @submitOrder="submitOrder"
    ></router-view>
  </div>
  <footer>
    <p>© 2025 Best Buy Electronics. All rights reserved.</p>
  </footer>
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
          console.log('success getting proxy products')
          this.products = products
        })
        .catch(error => {
          console.log(error)
          alert('Error occurred while fetching products')
        })
    },
    addToCart({ productId, quantity }) {
      const existingCartItem = this.cartItems.find(
        item => item.product.id == productId
      )
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
        items: this.cartItems.map(item => {
          return {
            productId: item.product.id,
            quantity: item.quantity,
            price: item.product.price
          }
        })
      }
      console.log(JSON.stringify(order));

      fetch(`/order`, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(order)
      })
        .then(response => {
          console.log(response)
          if (!response.ok) {
            alert('Error occurred while submitting order')
          } else {
            this.cartItems = []
            alert('Order submitted successfully')
          }
        })
        .catch(error => {
          console.log(error)
          alert('Error occurred while submitting order')
        })
    }
  },
}
</script>

<style>
/* Global Resets and Best Buy-ish Styles */
body {
  background-color: #f0f2f5; /* Light gray background */
  margin: 0;
  padding: 0;
  font-family: 'Human BBY', Arial, sans-serif; /* Mimic their font */
  color: #1d252c;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 80px; /* Space for fixed header */
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.main-container {
  flex: 1;
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  width: 100%;
  box-sizing: border-box;
}

footer {
  background-color: #f0f2f5;
  color: #555;
  padding: 2rem;
  border-top: 1px solid #ccc;
  margin-top: auto;
  font-size: 0.9rem;
}

button {
  cursor: pointer;
}

/* Common Utility for Links */
a {
  text-decoration: none;
  color: inherit;
}
</style>