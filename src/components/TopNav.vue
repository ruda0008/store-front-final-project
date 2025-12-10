<template>
  <nav>
    <div class="nav-container">
      <div class="logo">
        <a href="/">
           <span class="brand-text">Best Buy</span>
        </a>
      </div>
      
      <div class="search-bar">
        <input type="text" placeholder="Search for products, brands, and more">
        <button class="search-btn">🔍</button>
      </div>

      <button class="hamburger" @click="toggleNav">
        <span class="hamburger-icon"></span>
      </button>

      <ul class="nav-links" :class="{ 'nav-links--open': isNavOpen }">
        <li><router-link to="/" @click="closeNav">Deals</router-link></li>
        <li class="cart-link">
          <router-link to="/cart" @click="closeNav">
            🛒 Cart <span class="badge" v-if="cartItemCount > 0">{{ cartItemCount }}</span>
          </router-link>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'TopNav',
  props: ['cartItemCount'],
  data() {
    return {
      isNavOpen: false
    }
  },
  methods: {
    toggleNav() {
      this.isNavOpen = !this.isNavOpen
    },
    closeNav() {
      this.isNavOpen = false
    }
  }
}
</script>

<style scoped>
nav {
  background-color: #0046be; /* Best Buy Blue */
  color: #fff;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  height: 70px;
  display: flex;
  align-items: center;
  box-shadow: 0 2px 5px rgba(0,0,0,0.2);
}

.nav-container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 1rem;
}

.brand-text {
  font-size: 1.5rem;
  font-weight: 900;
  color: #fff;
  letter-spacing: -1px;
}

/* Search Bar Styling */
.search-bar {
  flex-grow: 1;
  margin: 0 2rem;
  display: flex;
  max-width: 600px;
}

.search-bar input {
  width: 100%;
  padding: 10px;
  border: none;
  border-radius: 4px 0 0 4px;
  font-size: 1rem;
}

.search-bar .search-btn {
  background-color: #fff;
  border: none;
  border-radius: 0 4px 4px 0;
  padding: 0 15px;
  cursor: pointer;
  font-size: 1.2rem;
}

.nav-links {
  display: flex;
  list-style: none;
  font-size: 1rem;
  font-weight: bold;
  margin: 0;
  padding: 0;
  align-items: center;
}

.nav-links li {
  margin-left: 1.5rem;
}

.nav-links a {
  color: #fff;
  text-decoration: none;
}

.nav-links a:hover {
  text-decoration: underline;
}

.cart-link a {
  display: flex;
  align-items: center;
}

.badge {
  background-color: #ffce00;
  color: #000;
  border-radius: 50%;
  padding: 2px 6px;
  font-size: 0.8rem;
  margin-left: 5px;
}

/* Hamburger menu styles remain mostly the same */
.hamburger {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
}

@media (max-width: 768px) {
  .search-bar {
    display: none; /* Hide search on mobile to save space */
  }
  
  .nav-links {
    display: none;
    position: absolute;
    top: 70px;
    left: 0;
    right: 0;
    background-color: #003da6;
    flex-direction: column;
    padding: 1rem;
  }

  .nav-links--open {
    display: flex;
  }
  
  .nav-links li {
    margin: 10px 0;
  }

  .hamburger {
    display: block;
  }
  
  .hamburger-icon {
    display: block;
    width: 25px;
    height: 3px;
    background-color: #fff;
    position: relative;
  }
}
</style>