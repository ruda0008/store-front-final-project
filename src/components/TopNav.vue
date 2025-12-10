<template>
  <nav class="bby-header">
    <div class="header-content">
      <div class="logo-area">
        <router-link to="/" class="bby-logo">
          <span class="logo-tag">BEST</span>
          <span class="logo-tag">PETS</span>
        </router-link>
      </div>

      <div class="search-container">
        <input type="text" placeholder="Search Best Pets" />
        <button class="search-icon-btn">
          <svg viewBox="0 0 24 24" width="20" height="20" fill="none" stroke="#0046be" stroke-width="2"><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></svg>
        </button>
      </div>

      <div class="header-actions">
        <div class="store-loc">
          <span class="icon">📍</span>
          <div class="text-group">
            <span class="loc-store">Ottawa</span>
            <span class="loc-status">Open until 9pm</span>
          </div>
        </div>
        
        <router-link to="/cart" class="cart-btn">
          <span class="cart-icon">🛒</span>
          <span class="cart-label">Cart</span>
          <span class="cart-badge" v-if="cartItemCount > 0">{{ cartItemCount }}</span>
        </router-link>
      </div>
    </div>
    
    <div class="bottom-strip">
        <ul class="strip-links">
            <li><a href="#">Top Deals</a></li>
            <li><a href="#">Deal of the Day</a></li>
            <li><a href="#">Totaltech Membership</a></li>
            <li><a href="#">Credit Cards</a></li>
            <li><a href="#">Gift Cards</a></li>
        </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'TopNav',
  props: ['cartItemCount']
}
</script>

<style scoped>
.bby-header {
  background-color: #0046be; /* Official Best Buy Blue */
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 9999;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}

.header-content {
  display: flex;
  align-items: center;
  height: 75px;
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 16px;
  gap: 20px;
}

/* LOGO */
.bby-logo {
  display: flex;
  flex-direction: column;
  line-height: 0.9;
  text-decoration: none;
  color: #000;
  background-color: #ffce00; /* Best Buy Tag Yellow */
  padding: 8px 12px;
  font-weight: 900;
  font-size: 20px;
  letter-spacing: -1px;
}

/* SEARCH */
.search-container {
  flex: 1;
  display: flex;
  height: 40px;
}

.search-container input {
  width: 100%;
  padding: 0 15px;
  font-size: 16px;
  border: none;
  border-radius: 4px 0 0 4px;
  outline: none;
}

.search-icon-btn {
  background: white;
  border: none;
  padding: 0 15px;
  border-radius: 0 4px 4px 0;
  cursor: pointer;
}

/* ACTIONS */
.header-actions {
  display: flex;
  align-items: center;
  color: white;
  gap: 25px;
}

.store-loc {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 13px;
  cursor: pointer;
}
.text-group {
    display: flex;
    flex-direction: column;
}
.loc-store { font-weight: 700; }

.cart-btn {
  display: flex;
  align-items: center;
  color: white;
  text-decoration: none;
  font-weight: 700;
  position: relative;
}

.cart-icon { font-size: 24px; margin-right: 5px; }
.cart-badge {
    position: absolute;
    top: -8px;
    right: -10px;
    background: #ffce00;
    color: black;
    border-radius: 50%;
    width: 20px;
    height: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 12px;
}

/* BOTTOM STRIP */
.bottom-strip {
    background-color: #003da6; /* Slightly darker blue */
    border-top: 1px solid rgba(255,255,255,0.2);
    height: 40px;
    display: flex;
    align-items: center;
}
.strip-links {
    list-style: none;
    display: flex;
    gap: 25px;
    margin: 0 auto;
    max-width: 1400px;
    padding: 0 16px;
    width: 100%;
    font-size: 14px;
    font-weight: 600;
}
.strip-links a { color: white; text-decoration: none; }
.strip-links a:hover { text-decoration: underline; }

@media(max-width: 768px) {
    .bottom-strip, .store-loc { display: none; }
    .header-content { gap: 10px; }
}
</style>