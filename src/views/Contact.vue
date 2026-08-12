<template>
  <div class="contact-page">
    <div class="container">
      <!-- Hero -->
      <div class="contact-hero">
        <h1>Contact Us</h1>
        <p>We'd love to hear from you. Get in touch with our team.</p>
      </div>

      <div class="contact-layout">
        <!-- Contact Form -->
        <div class="contact-form">
          <h2>Send Us a Message</h2>
          <form @submit.prevent="handleSubmit">
            <div class="form-row">
              <div class="form-group">
                <label>Your Name *</label>
                <input v-model="form.name" type="text" required placeholder="Full name" />
              </div>
              <div class="form-group">
                <label>Email *</label>
                <input v-model="form.email" type="email" required placeholder="your@email.com" />
              </div>
            </div>
            <div class="form-group">
              <label>Subject</label>
              <input v-model="form.subject" type="text" placeholder="What is this about?" />
            </div>
            <div class="form-group">
              <label>Message *</label>
              <textarea v-model="form.message" rows="6" required placeholder="Write your message here..."></textarea>
            </div>
            <button type="submit" class="btn-submit" :disabled="submitted">
              {{ submitted ? 'Message Sent!' : 'Send Message' }}
            </button>
          </form>
        </div>

        <!-- Contact Info -->
        <div class="contact-info">
          <div class="info-card">
            <div class="info-icon">🏢</div>
            <h3>Company</h3>
            <p>HOOSEEN (HONG KONG) TECHNOLOGY LIMITED</p>
            <p>Address:UNIT 1406B 14/F THE BELGIAN BANK BUILDING NOS 721-725NATHAN ROAD KOWLOON HONG KONG</p>
            <p>Full Name：He Feng</p>
            <p>Phone Number：65450369</p>
            <p>Email Address：info@hooseen.pro</p>

          </div>
          <div class="info-card">
            <div class="info-icon">🕐</div>
            <h3>Business Hours</h3>
            <p>Monday - Friday: 9:00 AM - 6:00 PM</p>
            <p>Saturday: 10:00 AM - 2:00 PM</p>
            <p>Sunday: Closed</p>
          </div>
          <div class="info-card">
            <div class="info-icon">💬</div>
            <h3>Get In Touch</h3>
            <p>Fill out the form and our team will get back to you within 24 hours.</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
import { ElMessage } from 'element-plus'

const submitted = ref(false)

const form = reactive({
  name: '',
  email: '',
  subject: '',
  message: ''
})

function handleSubmit() {
  console.log('Contact form submitted:', { ...form })
  ElMessage({
    message: 'Your message has been sent successfully! We will reply within 24 hours.',
    type: 'success',
    duration: 3000
  })
  submitted.value = true
  setTimeout(() => {
    submitted.value = false
    form.name = ''
    form.email = ''
    form.subject = ''
    form.message = ''
  }, 3000)
}
</script>

<style scoped>
.container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Hero */
.contact-hero {
  text-align: center;
  padding: 60px 0 40px;
  background: linear-gradient(135deg, #eff6ff 0%, #dbeafe 100%);
  border-radius: 16px;
  margin-bottom: 48px;
}

.contact-hero h1 {
  font-size: 40px;
  font-weight: 800;
  color: #111827;
  margin-bottom: 12px;
}

.contact-hero p {
  font-size: 18px;
  color: #4b5563;
}

/* Layout */
.contact-layout {
  display: grid;
  grid-template-columns: 1fr 380px;
  gap: 40px;
  align-items: start;
}

/* Form */
.contact-form {
  background: #fff;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 32px;
}

.contact-form h2 {
  font-size: 22px;
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

.btn-submit:hover:not(:disabled) {
  background: #1e40af;
}

.btn-submit:disabled {
  background: #10b981;
  cursor: default;
}

/* Contact Info */
.contact-info {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.info-card {
  background: #fff;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 24px;
}

.info-icon {
  font-size: 32px;
  margin-bottom: 12px;
}

.info-card h3 {
  font-size: 16px;
  font-weight: 600;
  color: #111827;
  margin-bottom: 8px;
}

.info-card p {
  font-size: 14px;
  color: #4b5563;
  line-height: 1.6;
}

.info-note {
  font-size: 12px;
  color: #9ca3af;
  margin-top: 4px;
}

/* Responsive */
@media (max-width: 1024px) {
  .contact-layout {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 768px) {
  .form-row {
    grid-template-columns: 1fr;
  }
  .contact-hero h1 {
    font-size: 28px;
  }
}
</style>
