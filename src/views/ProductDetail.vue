<template>
  <div class="product-detail" v-if="product">
    <div class="container">
      <!-- Breadcrumb -->
      <div class="breadcrumb">
        <router-link to="/">Home</router-link>
        <span>/</span>
        <router-link to="/products">Products</router-link>
        <span>/</span>
        <span class="current">{{ product.name }}</span>
      </div>

      <!-- Product Main -->
      <div class="product-main">
        <!-- Image Gallery -->
        <div class="product-gallery">
          <div class="main-image">
            <img :src="currentImage" :alt="product.name" />
          </div>
          <div class="thumbnail-list">
            <div
              v-for="(img, index) in product.images"
              :key="index"
              class="thumbnail"
              :class="{ active: currentImage === img }"
              @click="currentImage = img"
            >
              <img :src="img" :alt="`${product.name} ${index + 1}`" />
            </div>
          </div>
        </div>

        <!-- Product Info -->
        <div class="product-info">
          <h1 class="product-name">{{ product.name }}</h1>
          <div class="product-price">${{ product.price.toFixed(2) }}</div>

          <div class="info-list">
            <div class="info-item">
              <span class="info-label">MOQ:</span>
              <span class="info-value">{{ product.moq }} pcs</span>
            </div>
            <div class="info-item">
              <span class="info-label">Category:</span>
              <span class="info-value">{{ product.category }}</span>
            </div>
            <div class="info-item">
              <span class="info-label">Supply Ability:</span>
              <span class="info-value">{{ product.supplyAbility }}</span>
            </div>
            <div class="info-item">
              <span class="info-label">Payment Terms:</span>
              <span class="info-value">{{ product.paymentTerms }}</span>
            </div>
          </div>

          <!-- Quantity -->
          <div class="quantity-section">
            <label>Quantity:</label>
            <div class="quantity-control">
              <button @click="quantity = Math.max(product.moq, quantity - 1)">−</button>
              <input v-model.number="quantity" type="number" :min="product.moq" />
              <button @click="quantity++">+</button>
            </div>
            <span class="moq-hint">Min. order: {{ product.moq }} pcs</span>
          </div>

          <!-- Actions -->
          <div class="action-buttons">
            <button class="btn-cart" @click="handleAddToCart">🛒 Add To Cart</button>
            <button class="btn-inquiry" @click="handleInquiry">📩 Send Inquiry</button>
          </div>
        </div>
      </div>

      <!-- Product Details Tabs -->
      <div class="product-tabs">
        <div class="tab-headers">
          <button
            v-for="tab in tabs"
            :key="tab.key"
            class="tab-btn"
            :class="{ active: activeTab === tab.key }"
            @click="activeTab = tab.key"
          >
            {{ tab.label }}
          </button>
        </div>
        <div class="tab-content">
          <div v-if="activeTab === 'description'" class="tab-pane">
            <p>{{ product.description }}</p>
          </div>
          <div v-if="activeTab === 'specification'" class="tab-pane">
            <p>{{ product.specification }}</p>
          </div>
          <div v-if="activeTab === 'packaging'" class="tab-pane">
            <p>{{ product.packaging }}</p>
          </div>
          <div v-if="activeTab === 'shipping'" class="tab-pane">
            <p>{{ product.shipping }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Not Found -->
  <div v-else class="not-found">
    <div class="container">
      <h2>Product Not Found</h2>
      <router-link to="/products" class="btn-back">Back to Products</router-link>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { useCartStore } from '../store/cart'
import { ElMessage } from 'element-plus'
import { products } from '../data/products'

const route = useRoute()
const router = useRouter()
const cartStore = useCartStore()

const product = computed(() => products.find(p => p.id === Number(route.params.id)))
const currentImage = ref('')
const quantity = ref(1)
const activeTab = ref('description')

const tabs = [
  { key: 'description', label: 'Description' },
  { key: 'specification', label: 'Specification' },
  { key: 'packaging', label: 'Packaging' },
  { key: 'shipping', label: 'Shipping Information' }
]

watch(product, (p) => {
  if (p) {
    currentImage.value = p.images[0]
    quantity.value = p.moq
  }
}, { immediate: true })

function handleAddToCart() {
  if (product.value) {
    cartStore.addToCart(product.value, quantity.value)
    ElMessage({
      message: `${product.value.name} (x${quantity.value}) added to cart!`,
      type: 'success',
      duration: 2000
    })
  }
}

function handleInquiry() {
  if (product.value) {
    cartStore.addToCart(product.value, quantity.value)
    router.push('/checkout')
  }
}
</script>

<style scoped>
.container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Breadcrumb */
.breadcrumb {
  padding: 20px 0;
  font-size: 14px;
  color: #6b7280;
}

.breadcrumb a {
  color: #1a56db;
  text-decoration: none;
}

.breadcrumb span {
  margin: 0 8px;
}

.breadcrumb .current {
  color: #374151;
}

/* Product Main */
.product-main {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 48px;
  padding: 20px 0 48px;
}

/* Gallery */
.product-gallery {
  position: sticky;
  top: 90px;
}

.main-image {
  width: 100%;
  aspect-ratio: 1;
  border-radius: 12px;
  overflow: hidden;
  background: #f9fafb;
  margin-bottom: 16px;
}

.main-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.thumbnail-list {
  display: flex;
  gap: 12px;
}

.thumbnail {
  width: 80px;
  height: 80px;
  border-radius: 8px;
  overflow: hidden;
  cursor: pointer;
  border: 2px solid transparent;
  transition: border-color 0.2s;
}

.thumbnail.active,
.thumbnail:hover {
  border-color: #1a56db;
}

.thumbnail img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Product Info */
.product-name {
  font-size: 28px;
  font-weight: 700;
  color: #111827;
  margin-bottom: 16px;
  line-height: 1.3;
}

.product-price {
  font-size: 36px;
  font-weight: 800;
  color: #dc2626;
  margin-bottom: 24px;
}

.info-list {
  margin-bottom: 24px;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  overflow: hidden;
}

.info-item {
  display: flex;
  padding: 14px 20px;
  border-bottom: 1px solid #f3f4f6;
}

.info-item:last-child {
  border-bottom: none;
}

.info-label {
  width: 140px;
  font-weight: 600;
  color: #374151;
  font-size: 14px;
}

.info-value {
  flex: 1;
  color: #6b7280;
  font-size: 14px;
}

/* Quantity */
.quantity-section {
  margin-bottom: 24px;
}

.quantity-section label {
  display: block;
  font-weight: 600;
  color: #374151;
  margin-bottom: 8px;
}

.quantity-control {
  display: inline-flex;
  align-items: center;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  overflow: hidden;
}

.quantity-control button {
  width: 40px;
  height: 40px;
  background: #f9fafb;
  border: none;
  font-size: 18px;
  cursor: pointer;
  color: #374151;
}

.quantity-control button:hover {
  background: #e5e7eb;
}

.quantity-control input {
  width: 80px;
  height: 40px;
  border: none;
  text-align: center;
  font-size: 16px;
  font-weight: 600;
  outline: none;
  -moz-appearance: textfield;
}

.quantity-control input::-webkit-outer-spin-button,
.quantity-control input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}

.moq-hint {
  margin-left: 12px;
  font-size: 13px;
  color: #9ca3af;
}

/* Actions */
.action-buttons {
  display: flex;
  gap: 12px;
}

.btn-cart,
.btn-inquiry {
  flex: 1;
  padding: 14px 24px;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-cart {
  background: #1a56db;
  color: #fff;
}

.btn-cart:hover {
  background: #1e40af;
}

.btn-inquiry {
  background: #f59e0b;
  color: #fff;
}

.btn-inquiry:hover {
  background: #d97706;
}

/* Tabs */
.product-tabs {
  padding: 40px 0;
  border-top: 1px solid #e5e7eb;
}

.tab-headers {
  display: flex;
  gap: 0;
  border-bottom: 2px solid #e5e7eb;
}

.tab-btn {
  padding: 14px 24px;
  background: none;
  border: none;
  font-size: 15px;
  font-weight: 500;
  color: #6b7280;
  cursor: pointer;
  border-bottom: 2px solid transparent;
  margin-bottom: -2px;
  transition: all 0.2s;
}

.tab-btn:hover {
  color: #1a56db;
}

.tab-btn.active {
  color: #1a56db;
  border-bottom-color: #1a56db;
}

.tab-content {
  padding: 24px 0;
}

.tab-pane {
  font-size: 15px;
  line-height: 1.8;
  color: #4b5563;
}

/* Not Found */
.not-found {
  text-align: center;
  padding: 100px 20px;
}

.not-found h2 {
  font-size: 28px;
  color: #374151;
  margin-bottom: 16px;
}

.btn-back {
  display: inline-block;
  background: #1a56db;
  color: #fff;
  padding: 12px 24px;
  border-radius: 8px;
  text-decoration: none;
  font-weight: 600;
}

/* Responsive */
@media (max-width: 768px) {
  .product-main {
    grid-template-columns: 1fr;
    gap: 24px;
  }
  .product-gallery {
    position: static;
  }
  .product-name {
    font-size: 22px;
  }
  .product-price {
    font-size: 28px;
  }
  .action-buttons {
    flex-direction: column;
  }
  .tab-headers {
    overflow-x: auto;
  }
  .tab-btn {
    white-space: nowrap;
    padding: 12px 16px;
    font-size: 14px;
  }
}
</style>
