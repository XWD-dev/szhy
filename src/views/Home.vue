<template>
  <div class="home">
    <!-- Banner Section -->
    <section class="banner">
      <div class="banner-slider">
        <div class="banner-slide active">
          <div class="banner-overlay"></div>
          <div class="banner-content">
            <h1 class="banner-title">Premium Products</h1>
            <h2 class="banner-subtitle">Direct Factory Supply</h2>
            <p class="banner-desc">Competitive Prices · Global Shipping · Trusted by 10,000+ Buyers Worldwide</p>
            <div class="banner-buttons">
              <router-link to="/products" class="btn-primary">View Products</router-link>
              <router-link to="/contact" class="btn-outline">Contact Us</router-link>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Featured Products -->
    <section class="section featured-section">
      <div class="container">
        <h2 class="section-title">Featured Products</h2>
        <p class="section-subtitle">Explore our best-selling products with competitive wholesale prices</p>
        <div class="products-grid">
          <ProductCard v-for="product in featuredProducts" :key="product.id" :product="product" />
        </div>
        <div class="section-action">
          <router-link to="/products" class="btn-primary">View All Products</router-link>
        </div>
      </div>
    </section>

    <!-- Why Choose Us -->
    <section class="section advantages-section">
      <div class="container">
        <h2 class="section-title">Why Choose Us</h2>
        <p class="section-subtitle">We are committed to providing the best products and services</p>
        <div class="advantages-grid">
          <div class="advantage-card">
            <div class="advantage-icon">🏭</div>
            <h3>Factory Direct</h3>
            <p>Straight from our factory to you. No middlemen, no extra costs. Best wholesale prices guaranteed.</p>
          </div>
          <div class="advantage-card">
            <div class="advantage-icon">✅</div>
            <h3>Quality Guarantee</h3>
            <p>All products undergo strict quality control. ISO 9001 certified manufacturing process.</p>
          </div>
          <div class="advantage-card">
            <div class="advantage-icon">🌍</div>
            <h3>Global Shipping</h3>
            <p>We ship to 150+ countries worldwide. Fast and reliable delivery by sea, air, or express.</p>
          </div>
          <div class="advantage-card">
            <div class="advantage-icon">🔧</div>
            <h3>OEM / ODM Service</h3>
            <p>Custom design, logo printing, and packaging available. We bring your ideas to life.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA Section -->
    <section class="cta-section">
      <div class="container">
        <h2>Ready to Start Your Business?</h2>
        <p>Get a free quote today and enjoy exclusive wholesale discounts</p>
        <router-link to="/contact" class="btn-primary btn-lg">Get a Free Quote</router-link>
      </div>
    </section>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import ProductCard from '../components/ProductCard.vue'
import { products } from '../data/products'

const featuredProducts = computed(() => products.slice(0, 8))
</script>

<style scoped>
.container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Banner */
.banner {
  position: relative;
  background: linear-gradient(135deg, #0f172a 0%, #1e3a5f 50%, #1a56db 100%);
  min-height: 520px;
  display: flex;
  align-items: center;
  overflow: hidden;
}

.banner::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url('https://images.unsplash.com/photo-1586528116311-ad8dd3c8310d?w=1600&h=600&fit=crop') center/cover;
  opacity: 0.15;
}

.banner-slide {
  position: relative;
  width: 100%;
  z-index: 1;
}

.banner-content {
  max-width: 1280px;
  margin: 0 auto;
  padding: 80px 20px;
  text-align: center;
}

.banner-title {
  font-size: 52px;
  font-weight: 800;
  color: #fff;
  margin-bottom: 8px;
  letter-spacing: -1px;
}

.banner-subtitle {
  font-size: 28px;
  font-weight: 400;
  color: #93c5fd;
  margin-bottom: 20px;
}

.banner-desc {
  font-size: 18px;
  color: #bfdbfe;
  margin-bottom: 36px;
}

.banner-buttons {
  display: flex;
  gap: 16px;
  justify-content: center;
  flex-wrap: wrap;
}

.btn-primary {
  display: inline-block;
  background: #1a56db;
  color: #fff;
  padding: 14px 32px;
  border-radius: 8px;
  text-decoration: none;
  font-weight: 600;
  font-size: 16px;
  transition: all 0.2s;
}

.btn-primary:hover {
  background: #1e40af;
  transform: translateY(-1px);
}

.btn-outline {
  display: inline-block;
  background: transparent;
  color: #fff;
  padding: 14px 32px;
  border-radius: 8px;
  text-decoration: none;
  font-weight: 600;
  font-size: 16px;
  border: 2px solid #fff;
  transition: all 0.2s;
}

.btn-outline:hover {
  background: #fff;
  color: #1a56db;
}

.btn-lg {
  padding: 16px 40px;
  font-size: 18px;
}

/* Sections */
.section {
  padding: 80px 0;
}

.section-title {
  text-align: center;
  font-size: 32px;
  font-weight: 700;
  color: #111827;
  margin-bottom: 8px;
}

.section-subtitle {
  text-align: center;
  font-size: 16px;
  color: #6b7280;
  margin-bottom: 48px;
}

.section-action {
  text-align: center;
  margin-top: 40px;
}

/* Products Grid */
.products-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 24px;
}

/* Advantages */
.advantages-section {
  background: #f8fafc;
}

.advantages-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 24px;
}

.advantage-card {
  background: #fff;
  padding: 32px 24px;
  border-radius: 12px;
  text-align: center;
  transition: all 0.3s;
  border: 1px solid #e5e7eb;
}

.advantage-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
}

.advantage-icon {
  font-size: 48px;
  margin-bottom: 16px;
}

.advantage-card h3 {
  font-size: 18px;
  font-weight: 600;
  color: #111827;
  margin-bottom: 8px;
}

.advantage-card p {
  font-size: 14px;
  color: #6b7280;
  line-height: 1.6;
}

/* CTA */
.cta-section {
  background: linear-gradient(135deg, #1a56db 0%, #1e40af 100%);
  padding: 80px 0;
  text-align: center;
}

.cta-section h2 {
  font-size: 32px;
  font-weight: 700;
  color: #fff;
  margin-bottom: 12px;
}

.cta-section p {
  font-size: 18px;
  color: #bfdbfe;
  margin-bottom: 32px;
}

.cta-section .btn-primary {
  background: #fff;
  color: #1a56db;
}

.cta-section .btn-primary:hover {
  background: #f0f9ff;
}

/* Responsive */
@media (max-width: 1024px) {
  .products-grid {
    grid-template-columns: repeat(3, 1fr);
  }
  .advantages-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .banner-title {
    font-size: 32px;
  }
  .banner-subtitle {
    font-size: 20px;
  }
  .banner-desc {
    font-size: 15px;
  }
  .banner-content {
    padding: 60px 20px;
  }
  .products-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 16px;
  }
  .advantages-grid {
    grid-template-columns: 1fr;
  }
  .section {
    padding: 50px 0;
  }
  .section-title {
    font-size: 24px;
  }
}
</style>
