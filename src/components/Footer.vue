<template>
  <footer class="footer">
    <div class="footer-container">
      <div class="footer-grid">
        <!-- Company Info -->
        <div class="footer-col">
          <h3 class="footer-title">
            <span class="footer-logo-icon">🌐</span> HOOSEEN
          </h3>
          <p class="footer-desc">
            Your trusted partner for premium products at competitive factory-direct prices. We serve customers worldwide with quality products and reliable service.
          </p>
          <p class="footer-desc">
            Address:UNIT 1406B 14/F THE BELGIAN BANK BUILDING NOS 721-725NATHAN ROAD KOWLOON HONG KONG
          </p>
          <p class="footer-desc">Full Name：He Feng</p>
          <p class="footer-desc">Phone Number：65450369</p>
          <p class="footer-desc">Email Address：hosos253@yeah.net</p>

        </div>

        <!-- Quick Links -->
        <div class="footer-col">
          <h4 class="footer-subtitle">Quick Links</h4>
          <router-link to="/" class="footer-link">Home</router-link>
          <router-link to="/products" class="footer-link">Products</router-link>
          <router-link to="/about" class="footer-link">About Us</router-link>
          <router-link to="/contact" class="footer-link">Contact Us</router-link>
        </div>

        <!-- Categories -->
        <div class="footer-col">
          <h4 class="footer-subtitle">Categories</h4>
          <router-link to="/products?category=Electronics" class="footer-link">Electronics</router-link>
          <router-link to="/products?category=Lighting" class="footer-link">Lighting</router-link>
          <router-link to="/products?category=Tools" class="footer-link">Tools</router-link>
          <router-link to="/products?category=Home Products" class="footer-link">Home Products</router-link>
          <router-link to="/products?category=Outdoor Products" class="footer-link">Outdoor Products</router-link>
        </div>

        <!-- Contact Info -->
        <div class="footer-col">
          <h4 class="footer-subtitle">Contact Us</h4>
          <router-link to="/contact" class="footer-link">Send Us a Message</router-link>
          <router-link to="/contact" class="footer-link">Get a Free Quote</router-link>
        </div>
      </div>

      <div class="footer-bottom">
        <p>© {{ currentYear }} HOOSEEN. All Rights Reserved.</p>
      </div>
    </div>
  </footer>
</template>

<script setup>
const currentYear = new Date().getFullYear()
</script>

<style scoped>
.footer {
  background: #111827;
  color: #d1d5db;
  padding: 60px 0 0;
  margin-top: 60px;
}

.footer-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 20px;
}

.footer-grid {
  display: grid;
  grid-template-columns: 1.5fr 1fr 1fr 1.5fr;
  gap: 40px;
}

.footer-title {
  color: #fff;
  font-size: 20px;
  font-weight: 700;
  margin-bottom: 16px;
  display: flex;
  align-items: center;
  gap: 8px;
}

.footer-logo-icon {
  font-size: 24px;
}

.footer-desc {
  font-size: 14px;
  line-height: 1.7;
  color: #9ca3af;
}

.footer-subtitle {
  color: #fff;
  font-size: 16px;
  font-weight: 600;
  margin-bottom: 16px;
}

.footer-link {
  display: block;
  color: #9ca3af;
  text-decoration: none;
  font-size: 14px;
  padding: 4px 0;
  transition: color 0.2s;
}

.footer-link:hover {
  color: #60a5fa;
}

.contact-item {
  font-size: 14px;
  line-height: 1.8;
  color: #9ca3af;
}

.footer-bottom {
  margin-top: 40px;
  padding: 20px 0;
  border-top: 1px solid #1f2937;
  text-align: center;
  font-size: 13px;
  color: #6b7280;
}

@media (max-width: 768px) {
  .footer-grid {
    grid-template-columns: 1fr;
    gap: 30px;
  }
}
</style>
