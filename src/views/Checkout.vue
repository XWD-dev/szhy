<template>
  <div class="checkout-page">
    <div class="container">
      <h1 class="page-title">Checkout / Send Inquiry</h1>

      <div v-if="!submitted" class="checkout-layout">
        <!-- Inquiry Form -->
        <div class="checkout-form">
          <h2>Contact Information</h2>
          <form @submit.prevent="handleSubmit">
            <div class="form-row">
              <div class="form-group">
                <label>Company Name *</label>
                <input v-model="form.companyName" type="text" required placeholder="Your company name" />
              </div>
              <div class="form-group">
                <label>Contact Person *</label>
                <input v-model="form.contactPerson" type="text" required placeholder="Full name" />
              </div>
            </div>
            <div class="form-row">
              <div class="form-group">
                <label>Email *</label>
                <input v-model="form.email" type="email" required placeholder="your@email.com" />
              </div>
              <div class="form-group">
                <label>Country *</label>
                <input v-model="form.country" type="text" required placeholder="Your country" />
              </div>
            </div>
            <div class="form-group">
              <label>Shipping Address</label>
              <input v-model="form.address" type="text" placeholder="Full shipping address" />
            </div>
            <div class="form-group">
              <label>Product Requirement</label>
              <textarea v-model="form.requirement" rows="3" placeholder="Describe your product requirements..."></textarea>
            </div>
            <div class="form-group">
              <label>Message</label>
              <textarea v-model="form.message" rows="4" placeholder="Additional notes or questions..."></textarea>
            </div>
            <button type="submit" class="btn-submit">Submit Inquiry</button>
          </form>
        </div>

        <!-- Order Summary -->
        <div class="checkout-summary">
          <h3>Inquiry Items</h3>
          <div v-for="item in cartStore.items" :key="item.id" class="summary-item">
            <img :src="item.image" :alt="item.name" />
            <div class="item-details">
              <span class="item-name">{{ item.name }}</span>
              <span class="item-qty">Qty: {{ item.quantity }}</span>
            </div>
            <span class="item-subtotal">${{ (item.price * item.quantity).toFixed(2) }}</span>
          </div>
          <div class="summary-total">
            <span>Total Estimated</span>
            <span>${{ cartStore.totalPrice.toFixed(2) }}</span>
          </div>
          <p class="summary-note">* Final pricing will be confirmed by our sales team after reviewing your inquiry.</p>
        </div>
      </div>

      <!-- Success State -->
      <div v-else class="success-state">
        <div class="success-icon">✅</div>
        <h2>Thank you!</h2>
        <p>Our sales team will contact you soon.</p>
        <p class="success-detail">We have received your inquiry and will respond within 24 hours.</p>
        <router-link to="/" class="btn-primary">Back to Home</router-link>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
import { useCartStore } from '../store/cart'

const cartStore = useCartStore()
const submitted = ref(false)

const form = reactive({
  companyName: '',
  contactPerson: '',
  email: '',
  country: '',
  address: '',
  requirement: '',
  message: ''
})

function handleSubmit() {
  // In real app, this would send data to backend
  console.log('Inquiry submitted:', { ...form, items: cartStore.items })
  submitted.value = true
  cartStore.clearCart()
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

.checkout-layout {
  display: grid;
  grid-template-columns: 1fr 400px;
  gap: 32px;
  align-items: start;
}

/* Form */
.checkout-form {
  background: #fff;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 32px;
}

.checkout-form h2 {
  font-size: 20px;
  font-weight: 600;
  color: #111827;
  margin-bottom: 24px;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  font-size: 14px;
  font-weight: 600;
  color: #374151;
  margin-bottom: 6px;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 12px 16px;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  font-size: 14px;
  color: #111827;
  outline: none;
  transition: border-color 0.2s;
  font-family: inherit;
}

.form-group input:focus,
.form-group textarea:focus {
  border-color: #1a56db;
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: #9ca3af;
}

.btn-submit {
  width: 100%;
  padding: 14px;
  background: #1a56db;
  color: #fff;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s;
}

.btn-submit:hover {
  background: #1e40af;
}

/* Summary */
.checkout-summary {
  background: #fff;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 24px;
  position: sticky;
  top: 90px;
}

.checkout-summary h3 {
  font-size: 18px;
  font-weight: 600;
  color: #111827;
  margin-bottom: 20px;
}

.summary-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 0;
  border-bottom: 1px solid #f3f4f6;
}

.summary-item img {
  width: 50px;
  height: 50px;
  object-fit: cover;
  border-radius: 6px;
  background: #f9fafb;
}

.item-details {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.item-name {
  font-size: 14px;
  font-weight: 500;
  color: #111827;
}

.item-qty {
  font-size: 12px;
  color: #9ca3af;
}

.item-subtotal {
  font-weight: 600;
  font-size: 14px;
  color: #111827;
}

.summary-total {
  display: flex;
  justify-content: space-between;
  padding: 16px 0;
  margin-top: 8px;
  border-top: 2px solid #e5e7eb;
  font-weight: 700;
  font-size: 18px;
  color: #111827;
}

.summary-note {
  font-size: 12px;
  color: #9ca3af;
  margin-top: 12px;
  line-height: 1.5;
}

/* Success */
.success-state {
  text-align: center;
  padding: 80px 20px;
}

.success-icon {
  font-size: 72px;
  margin-bottom: 16px;
}

.success-state h2 {
  font-size: 32px;
  font-weight: 700;
  color: #111827;
  margin-bottom: 12px;
}

.success-state p {
  font-size: 18px;
  color: #4b5563;
  margin-bottom: 8px;
}

.success-detail {
  font-size: 14px;
  color: #9ca3af;
  margin-bottom: 32px;
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
  .checkout-layout {
    grid-template-columns: 1fr;
  }
  .checkout-summary {
    position: static;
  }
}

@media (max-width: 768px) {
  .form-row {
    grid-template-columns: 1fr;
  }
  .page-title {
    font-size: 24px;
  }
}
</style>
