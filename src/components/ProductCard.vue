<template>
  <div class="product-card" @click="goToDetail">
    <div class="card-image">
      <img :src="product.image" :alt="product.name" loading="lazy" />
      <span class="card-category">{{ product.category }}</span>
    </div>
    <div class="card-body">
      <h3 class="card-title">{{ product.name }}</h3>
      <div class="card-price">${{ product.price.toFixed(2) }}</div>
      <div class="card-moq">MOQ: {{ product.moq }} pcs</div>
      <button class="card-btn" @click.stop="handleAddToCart">
        Add To Cart
      </button>
    </div>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'
import { useCartStore } from '../store/cart'
import { ElMessage } from 'element-plus'

const props = defineProps({
  product: { type: Object, required: true }
})

const router = useRouter()
const cartStore = useCartStore()

function goToDetail() {
  router.push(`/product/${props.product.id}`)
}

function handleAddToCart() {
  cartStore.addToCart(props.product)
  ElMessage({
    message: `${props.product.name} added to cart!`,
    type: 'success',
    duration: 2000
  })
}
</script>

<style scoped>
.product-card {
  background: #fff;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.06);
  transition: all 0.3s;
  cursor: pointer;
}

.product-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
}

.card-image {
  position: relative;
  padding-top: 100%;
  overflow: hidden;
  background: #f9fafb;
}

.card-image img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s;
}

.product-card:hover .card-image img {
  transform: scale(1.05);
}

.card-category {
  position: absolute;
  top: 12px;
  left: 12px;
  background: #1a56db;
  color: #fff;
  font-size: 11px;
  font-weight: 600;
  padding: 4px 10px;
  border-radius: 12px;
}

.card-body {
  padding: 16px;
}

.card-title {
  font-size: 15px;
  font-weight: 600;
  color: #1f2937;
  margin-bottom: 8px;
  line-height: 1.4;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.card-price {
  font-size: 20px;
  font-weight: 700;
  color: #dc2626;
  margin-bottom: 4px;
}

.card-moq {
  font-size: 12px;
  color: #6b7280;
  margin-bottom: 12px;
}

.card-btn {
  width: 100%;
  padding: 10px;
  background: #1a56db;
  color: #fff;
  border: none;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s;
}

.card-btn:hover {
  background: #1e40af;
}
</style>
