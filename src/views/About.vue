<template>
  <div class="about-page">
    <div class="container">
      <!-- Hero -->
      <div class="about-hero">
        <h1>About Us</h1>
        <p>HOOSEEN — Your trusted partner for premium products</p>
      </div>

      <!-- What We Offer -->
      <section class="about-section">
        <div class="section-content">
          <h2>What We Offer</h2>
          <p>
            HOOSEEN is a professional supplier of high-quality consumer products.
            We work directly with factories to bring you the best products at competitive wholesale prices.
          </p>
          <ul class="capability-list">
            <li>Factory-direct pricing with no middlemen</li>
            <li>Wide range of product categories</li>
            <li>OEM and ODM customization available</li>
            <li>Flexible minimum order quantities</li>
            <li>Fast and reliable global shipping</li>
          </ul>
        </div>
        <div class="section-image">
          <img src="https://images.unsplash.com/photo-1586528116311-ad8dd3c8310d?w=600&h=400&fit=crop" alt="Products" />
        </div>
      </section>

      <!-- Our Commitment -->
      <section class="about-section reverse">
        <div class="section-image">
          <img src="https://images.unsplash.com/photo-1581091226825-a6a2a5aee158?w=600&h=400&fit=crop" alt="Quality" />
        </div>
        <div class="section-content">
          <h2>Our Commitment</h2>
          <p>
            Every product we supply goes through strict quality inspection before shipping.
            We are committed to delivering reliable products and excellent service to our customers worldwide.
          </p>
          <ul class="capability-list">
            <li>Strict quality control process</li>
            <li>Professional packaging and labeling</li>
            <li>Timely delivery and order tracking</li>
            <li>Responsive customer support</li>
            <li>After-sales service guarantee</li>
          </ul>
        </div>
      </section>

      <!-- Stats -->
      <section class="stats-section">
        <h2>Our Numbers</h2>
        <div class="stats-grid">
          <div class="stat-card">
            <div class="stat-number">500+</div>
            <div class="stat-label">Product SKUs</div>
          </div>
          <div class="stat-card">
            <div class="stat-number">50+</div>
            <div class="stat-label">Countries Served</div>
          </div>
          <div class="stat-card">
            <div class="stat-number">1000+</div>
            <div class="stat-label">Happy Customers</div>
          </div>
          <div class="stat-card">
            <div class="stat-number">99%</div>
            <div class="stat-label">Satisfaction Rate</div>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 20px;
}

.about-hero {
  text-align: center;
  padding: 60px 0 40px;
  background: linear-gradient(135deg, #eff6ff 0%, #dbeafe 100%);
  border-radius: 16px;
  margin-bottom: 60px;
}

.about-hero h1 {
  font-size: 40px;
  font-weight: 800;
  color: #111827;
  margin-bottom: 12px;
}

.about-hero p {
  font-size: 18px;
  color: #4b5563;
}

.about-section {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 48px;
  align-items: center;
  margin-bottom: 60px;
}

.about-section.reverse {
  direction: rtl;
}

.about-section.reverse > * {
  direction: ltr;
}

.section-content h2 {
  font-size: 28px;
  font-weight: 700;
  color: #111827;
  margin-bottom: 16px;
}

.section-content p {
  font-size: 15px;
  line-height: 1.8;
  color: #4b5563;
  margin-bottom: 16px;
}

.section-image img {
  width: 100%;
  border-radius: 12px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
}

.capability-list {
  list-style: none;
  padding: 0;
}

.capability-list li {
  padding: 8px 0;
  font-size: 15px;
  color: #374151;
  position: relative;
  padding-left: 24px;
}

.capability-list li::before {
  content: '✓';
  position: absolute;
  left: 0;
  color: #1a56db;
  font-weight: 700;
}

.stats-section {
  text-align: center;
  padding: 60px 0;
  margin-bottom: 20px;
}

.stats-section h2 {
  font-size: 28px;
  font-weight: 700;
  color: #111827;
  margin-bottom: 40px;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 24px;
}

.stat-card {
  padding: 32px 20px;
  background: linear-gradient(135deg, #1a56db 0%, #1e40af 100%);
  border-radius: 12px;
  color: #fff;
}

.stat-number {
  font-size: 40px;
  font-weight: 800;
  margin-bottom: 8px;
}

.stat-label {
  font-size: 15px;
  opacity: 0.9;
}

@media (max-width: 768px) {
  .about-section {
    grid-template-columns: 1fr;
    gap: 24px;
  }
  .about-section.reverse {
    direction: ltr;
  }
  .about-hero h1 {
    font-size: 28px;
  }
  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
  }
  .stat-number {
    font-size: 28px;
  }
}
</style>
