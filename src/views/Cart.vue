<template>
  <div class="cart-page">
    <div class="container">
      <h1 class="page-title">Shopping Cart</h1>

      <div v-if="cartStore.items.length > 0" class="cart-layout">
        <!-- Cart Items -->
        <div class="cart-items">
          <div class="cart-table">
            <div class="cart-header">
              <span class="col-product">Product</span>
              <span class="col-price">Price</span>
              <span class="col-qty">Quantity</span>
              <span class="col-subtotal">Subtotal</span>
              <span class="col-action"></span>
            </div>
            <div v-for="item in cartStore.items" :key="item.id" class="cart-row">
              <div class="col-product">
                <img :src="item.image" :alt="item.name" />
                <div class="product-info">
                  <router-link :to="`/product/${item.id}`" class="product-name">{{ item.name }}</router-link>
                  <span class="product-category">{{ item.category }}</span>
                </div>
              </div>
              <div class="col-price">${{ item.price.toFixed(2) }}</div>
              <div class="col-qty">
                <div class="qty-control">
                  <button @click="updateQty(item.id, item.quantity - 1)">−</button>
                  <span>{{ item.quantity }}</span>
                  <button @click="updateQty(item.id, item.quantity + 1)">+</button>
                </div>
              </div>
              <div class="col-subtotal">${{ (item.price * item.quantity).toFixed(2) }}</div>
              <div class="col-action">
                <button class="btn-delete" @click="cartStore.removeFromCart(item.id)">✕</button>
              </div>
            </div>
          </div>
        </div>

        <!-- Cart Summary -->
        <div class="cart-summary">
          <h3>Order Summary</h3>
          <div class="summary-row">
            <span>Items</span>
            <span>{{ cartStore.totalItems }}</span>
          </div>
          <div class="summary-row total">
            <span>Total Amount</span>
            <span>${{ cartStore.totalPrice.toFixed(2) }}</span>
          </div>
          <div class="summary-actions">
            <router-link to="/products" class="btn-continue">Continue Shopping</router-link>
            <router-link to="/checkout" class="btn-checkout">Proceed Checkout</router-link>
          </div>
        </div>
      </div>

      <!-- Empty Cart -->
      <div v-else class="empty-cart">
        <div class="empty-icon">🛒</div>
        <h2>Your cart is empty</h2>
        <p>Browse our products and add items to your cart</p>
        <router-link to="/products" class="btn-primary">Start Shopping</router-link>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useCartStore } from '../store/cart'

const cartStore = useCartStore()

function updateQty(id, qty) {
  cartStore.updateQuantity(id, qty)
}
</script>

<style scoped>
.container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 20px;
}

.page-title {
  font-size: 32px;
  font-weight: 700;
  color: #111827;
  padding: 40px 0 24px;
}

.cart-layout {
  display: grid;
  grid-template-columns: 1fr 360px;
  gap: 32px;
  align-items: start;
}

/* Cart Table */
.cart-items {
  background: #fff;
  border-radius: 12px;
  border: 1px solid #e5e7eb;
  overflow: hidden;
}

.cart-header {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1fr 50px;
  gap: 16px;
  padding: 16px 20px;
  background: #f8fafc;
  font-weight: 600;
  font-size: 14px;
  color: #6b7280;
}

.cart-row {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1fr 50px;
  gap: 16px;
  padding: 20px;
  align-items: center;
  border-bottom: 1px solid #f3f4f6;
}

.cart-row:last-child {
  border-bottom: none;
}

.col-product {
  display: flex;
  align-items: center;
  gap: 16px;
}

.col-product img {
  width: 80px;
  height: 80px;
  object-fit: cover;
  border-radius: 8px;
  background: #f9fafb;
}

.product-info {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.product-name {
  font-weight: 600;
  color: #111827;
  text-decoration: none;
  font-size: 15px;
}

.product-name:hover {
  color: #1a56db;
}

.product-category {
  font-size: 12px;
  color: #9ca3af;
}

.col-price {
  font-size: 15px;
  color: #374151;
}

.qty-control {
  display: inline-flex;
  align-items: center;
  border: 1px solid #e5e7eb;
  border-radius: 6px;
}

.qty-control button {
  width: 32px;
  height: 32px;
  background: #f9fafb;
  border: none;
  font-size: 16px;
  cursor: pointer;
  color: #374151;
}

.qty-control button:hover {
  background: #e5e7eb;
}

.qty-control span {
  width: 48px;
  text-align: center;
  font-weight: 600;
  font-size: 14px;
}

.col-subtotal {
  font-weight: 600;
  color: #111827;
  font-size: 15px;
}

.btn-delete {
  background: none;
  border: none;
  font-size: 18px;
  color: #9ca3af;
  cursor: pointer;
  padding: 4px;
}

.btn-delete:hover {
  color: #ef4444;
}

/* Cart Summary */
.cart-summary {
  background: #fff;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 24px;
  position: sticky;
  top: 90px;
}

.cart-summary h3 {
  font-size: 18px;
  font-weight: 600;
  color: #111827;
  margin-bottom: 20px;
}

.summary-row {
  display: flex;
  justify-content: space-between;
  padding: 12px 0;
  font-size: 15px;
  color: #4b5563;
  border-bottom: 1px solid #f3f4f6;
}

.summary-row.total {
  font-weight: 700;
  font-size: 18px;
  color: #111827;
  border-bottom: none;
  padding: 16px 0;
}

.summary-actions {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-top: 20px;
}

.btn-continue {
  display: block;
  text-align: center;
  padding: 12px;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  color: #374151;
  text-decoration: none;
  font-weight: 600;
  font-size: 14px;
  transition: all 0.2s;
}

.btn-continue:hover {
  border-color: #1a56db;
  color: #1a56db;
}

.btn-checkout {
  display: block;
  text-align: center;
  padding: 14px;
  background: #1a56db;
  color: #fff;
  border-radius: 8px;
  text-decoration: none;
  font-weight: 600;
  font-size: 15px;
  transition: background 0.2s;
}

.btn-checkout:hover {
  background: #1e40af;
}

/* Empty Cart */
.empty-cart {
  text-align: center;
  padding: 80px 20px;
}

.empty-icon {
  font-size: 72px;
  margin-bottom: 16px;
}

.empty-cart h2 {
  font-size: 24px;
  color: #374151;
  margin-bottom: 8px;
}

.empty-cart p {
  font-size: 15px;
  color: #6b7280;
  margin-bottom: 24px;
}

.btn-primary {
  display: inline-block;
  background: #1a56db;
  color: #fff;
  padding: 14px 32px;
  border-radius: 8px;
  text-decoration: none;
  font-weight: 600;
}

.btn-primary:hover {
  background: #1e40af;
}

/* Responsive */
@media (max-width: 1024px) {
  .cart-layout {
    grid-template-columns: 1fr;
  }
  .cart-summary {
    position: static;
  }
}

@media (max-width: 768px) {
  .cart-header {
    display: none;
  }
  .cart-row {
    grid-template-columns: 1fr;
    gap: 12px;
  }
  .col-product img {
    width: 60px;
    height: 60px;
  }
}
</style>
