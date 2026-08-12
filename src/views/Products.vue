<template>
  <div class="products-page">
    <div class="container">
      <!-- Page Header -->
      <div class="page-header">
        <h1>Our Products</h1>
        <p>Discover premium quality products at competitive wholesale prices</p>
      </div>

      <!-- Filter Bar -->
      <div class="filter-bar">
        <div class="filter-left">
          <div class="search-input">
            <span class="search-icon">🔍</span>
            <input
              v-model="searchQuery"
              type="text"
              placeholder="Search products..."
              @input="handleSearch"
            />
          </div>
        </div>
        <div class="filter-right">
          <div class="category-filter">
            <select v-model="selectedCategory" @change="handleFilter">
              <option v-for="cat in categories" :key="cat" :value="cat">{{ cat }}</option>
            </select>
          </div>
          <div class="sort-filter">
            <select v-model="sortBy" @change="handleFilter">
              <option value="default">Sort By</option>
              <option value="price-low">Price: Low to High</option>
              <option value="price-high">Price: High to Low</option>
            </select>
          </div>
        </div>
      </div>

      <!-- Results Count -->
      <div class="results-count">
        <span>{{ filteredProducts.length }} products found</span>
      </div>

      <!-- Products Grid -->
      <div v-if="filteredProducts.length > 0" class="products-grid">
        <ProductCard v-for="product in filteredProducts" :key="product.id" :product="product" />
      </div>

      <!-- Empty State -->
      <div v-else class="empty-state">
        <div class="empty-icon">📦</div>
        <h3>No products found</h3>
        <p>Try adjusting your search or filter criteria</p>
        <button class="btn-reset" @click="resetFilters">Reset Filters</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import ProductCard from '../components/ProductCard.vue'
import { products, categories } from '../data/products'

const route = useRoute()

const searchQuery = ref('')
const selectedCategory = ref('All')
const sortBy = ref('default')

onMounted(() => {
  if (route.query.search) {
    searchQuery.value = route.query.search
  }
  if (route.query.category) {
    selectedCategory.value = route.query.category
  }
})

const filteredProducts = computed(() => {
  let result = [...products]

  // Filter by search
  if (searchQuery.value.trim()) {
    const query = searchQuery.value.toLowerCase()
    result = result.filter(p =>
      p.name.toLowerCase().includes(query) ||
      p.category.toLowerCase().includes(query) ||
      p.description.toLowerCase().includes(query)
    )
  }

  // Filter by category
  if (selectedCategory.value !== 'All') {
    result = result.filter(p => p.category === selectedCategory.value)
  }

  // Sort
  if (sortBy.value === 'price-low') {
    result.sort((a, b) => a.price - b.price)
  } else if (sortBy.value === 'price-high') {
    result.sort((a, b) => b.price - a.price)
  }

  return result
})

function handleSearch() {
  // reactive via computed
}

function handleFilter() {
  // reactive via computed
}

function resetFilters() {
  searchQuery.value = ''
  selectedCategory.value = 'All'
  sortBy.value = 'default'
}
</script>

<style scoped>
.container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 20px;
}

.page-header {
  text-align: center;
  padding: 48px 0 32px;
}

.page-header h1 {
  font-size: 36px;
  font-weight: 700;
  color: #111827;
  margin-bottom: 8px;
}

.page-header p {
  font-size: 16px;
  color: #6b7280;
}

/* Filter Bar */
.filter-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 16px;
  padding: 20px;
  background: #f8fafc;
  border-radius: 12px;
  margin-bottom: 24px;
  flex-wrap: wrap;
}

.filter-left {
  flex: 1;
  min-width: 200px;
}

.search-input {
  display: flex;
  align-items: center;
  background: #fff;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  padding: 0 12px;
}

.search-icon {
  font-size: 16px;
  margin-right: 8px;
}

.search-input input {
  border: none;
  outline: none;
  padding: 10px 0;
  font-size: 14px;
  width: 100%;
}

.filter-right {
  display: flex;
  gap: 12px;
}

.category-filter select,
.sort-filter select {
  padding: 10px 16px;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  font-size: 14px;
  color: #374151;
  background: #fff;
  cursor: pointer;
  outline: none;
}

.category-filter select:focus,
.sort-filter select:focus {
  border-color: #1a56db;
}

.results-count {
  font-size: 14px;
  color: #6b7280;
  margin-bottom: 20px;
}

/* Products Grid */
.products-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 24px;
}

/* Empty State */
.empty-state {
  text-align: center;
  padding: 80px 20px;
}

.empty-icon {
  font-size: 64px;
  margin-bottom: 16px;
}

.empty-state h3 {
  font-size: 20px;
  color: #374151;
  margin-bottom: 8px;
}

.empty-state p {
  font-size: 14px;
  color: #6b7280;
  margin-bottom: 24px;
}

.btn-reset {
  background: #1a56db;
  color: #fff;
  border: none;
  padding: 10px 24px;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
}

.btn-reset:hover {
  background: #1e40af;
}

@media (max-width: 1024px) {
  .products-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media (max-width: 768px) {
  .products-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 16px;
  }
  .filter-bar {
    flex-direction: column;
    align-items: stretch;
  }
  .filter-right {
    flex-direction: column;
  }
  .page-header h1 {
    font-size: 28px;
  }
}
</style>
