<template>
  <header class="header">
    <div class="header-container">
      <!-- Logo -->
      <router-link to="/" class="logo">
        <span class="logo-icon">🌐</span>
        <span class="logo-text">HOOSEEN</span>
      </router-link>

      <!-- Desktop Navigation -->
      <nav class="nav-desktop">
        <router-link to="/" class="nav-link" :class="{ active: $route.path === '/' }">Home</router-link>
        <router-link to="/products" class="nav-link" :class="{ active: $route.path === '/products' }">Products</router-link>
        <router-link to="/about" class="nav-link" :class="{ active: $route.path === '/about' }">About Us</router-link>
        <router-link to="/contact" class="nav-link" :class="{ active: $route.path === '/contact' }">Contact Us</router-link>
      </nav>

      <!-- Right Actions -->
      <div class="header-actions">
        <div class="search-box" :class="{ expanded: searchExpanded }">
          <input
            v-model="searchQuery"
            type="text"
            placeholder="Search products..."
            @keyup.enter="handleSearch"
            @blur="searchExpanded = false"
            ref="searchInput"
          />
          <button class="search-btn" @click="toggleSearch">
            <span>🔍</span>
          </button>
        </div>
        <router-link to="/cart" class="cart-link">
          <span class="cart-icon">🛒</span>
          <span v-if="cartStore.totalItems > 0" class="cart-badge">{{ cartStore.totalItems }}</span>
        </router-link>
        <!-- Mobile Menu Toggle -->
        <button class="mobile-menu-btn" @click="mobileMenuOpen = !mobileMenuOpen">
          <span>☰</span>
        </button>
      </div>
    </div>

    <!-- Mobile Navigation -->
    <nav v-if="mobileMenuOpen" class="nav-mobile">
      <router-link to="/" class="nav-link-mobile" @click="mobileMenuOpen = false">Home</router-link>
      <router-link to="/products" class="nav-link-mobile" @click="mobileMenuOpen = false">Products</router-link>
      <router-link to="/about" class="nav-link-mobile" @click="mobileMenuOpen = false">About Us</router-link>
      <router-link to="/contact" class="nav-link-mobile" @click="mobileMenuOpen = false">Contact Us</router-link>
      <router-link to="/cart" class="nav-link-mobile" @click="mobileMenuOpen = false">Cart ({{ cartStore.totalItems }})</router-link>
    </nav>
  </header>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { useCartStore } from '../store/cart'

const router = useRouter()
const cartStore = useCartStore()

const searchQuery = ref('')
const searchExpanded = ref(false)
const mobileMenuOpen = ref(false)
const searchInput = ref(null)

function toggleSearch() {
  if (searchExpanded.value && searchQuery.value) {
    handleSearch()
  } else {
    searchExpanded.value = true
    setTimeout(() => searchInput.value?.focus(), 100)
  }
}

function handleSearch() {
  if (searchQuery.value.trim()) {
    router.push({ path: '/products', query: { search: searchQuery.value.trim() } })
    searchQuery.value = ''
    searchExpanded.value = false
  }
}
</script>

<style scoped>
.header {
  background: #fff;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.08);
  position: sticky;
  top: 0;
  z-index: 1000;
}

.header-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 20px;
  height: 70px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.logo {
  display: flex;
  align-items: center;
  text-decoration: none;
  gap: 8px;
}

.logo-icon {
  font-size: 28px;
}

.logo-text {
  font-size: 18px;
  font-weight: 700;
  color: #1a56db;
  letter-spacing: -0.3px;
  white-space: nowrap;
}

.nav-desktop {
  display: flex;
  gap: 32px;
}

.nav-link {
  text-decoration: none;
  color: #4b5563;
  font-weight: 500;
  font-size: 15px;
  padding: 8px 0;
  border-bottom: 2px solid transparent;
  transition: all 0.2s;
}

.nav-link:hover,
.nav-link.active {
  color: #1a56db;
  border-bottom-color: #1a56db;
}

.header-actions {
  display: flex;
  align-items: center;
  gap: 16px;
}

.search-box {
  display: flex;
  align-items: center;
  border: 1px solid #e5e7eb;
  border-radius: 24px;
  overflow: hidden;
  transition: all 0.3s;
}

.search-box.expanded {
  border-color: #1a56db;
}

.search-box input {
  border: none;
  outline: none;
  padding: 8px 16px;
  font-size: 14px;
  width: 0;
  transition: width 0.3s;
}

.search-box.expanded input {
  width: 200px;
}

.search-btn {
  background: none;
  border: none;
  padding: 8px 12px;
  cursor: pointer;
  font-size: 18px;
}

.cart-link {
  position: relative;
  text-decoration: none;
  font-size: 22px;
  padding: 4px;
}

.cart-badge {
  position: absolute;
  top: -4px;
  right: -8px;
  background: #ef4444;
  color: #fff;
  font-size: 11px;
  font-weight: 700;
  min-width: 18px;
  height: 18px;
  border-radius: 9px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 4px;
}

.mobile-menu-btn {
  display: none;
  background: none;
  border: none;
  font-size: 24px;
  cursor: pointer;
  padding: 4px;
}

.nav-mobile {
  display: none;
  flex-direction: column;
  background: #fff;
  border-top: 1px solid #e5e7eb;
  padding: 12px 20px;
}

.nav-link-mobile {
  text-decoration: none;
  color: #4b5563;
  font-weight: 500;
  font-size: 15px;
  padding: 12px 0;
  border-bottom: 1px solid #f3f4f6;
}

@media (max-width: 768px) {
  .nav-desktop {
    display: none;
  }

  .mobile-menu-btn {
    display: block;
  }

  .nav-mobile {
    display: flex;
  }

  .search-box input {
    width: 120px;
  }

  .search-box.expanded input {
    width: 150px;
  }
}
</style>
