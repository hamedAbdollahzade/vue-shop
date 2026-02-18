<template>
  <MainLayout>
    <h2 class="text-2xl font-semibold mb-6">
      Products
    </h2>

    <div class="flex flex-col md:flex-row gap-4 mb-6">

      <!-- Search -->
      <input
        v-model="searchQuery"
        type="text"
        placeholder="Search products..."
        class="border rounded px-4 py-2 w-full md:w-1/2"
      />

      <!-- Category Filter -->
      <select
        v-model="selectedCategory"
        class="border rounded px-4 py-2 w-full md:w-1/3"
      >
        <option
          v-for="category in categories"
          :key="category"
          :value="category"
        >
          {{ category }}
        </option>
      </select>

    </div>


    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
      <ProductCard
        v-for="product in filteredProducts"
        :key="product.id"
        :product="product"
      />
    </div>
  </MainLayout>
</template>

<script setup>
import {ref, computed} from 'vue'
import {products} from '../data/products'
import MainLayout from '../layouts/MainLayout.vue'
import ProductCard from '../components/ProductCard.vue'


const searchQuery = ref('')
const selectedCategory = ref('all')

const categories = computed(() => {
  const unique = [...new Set(products.map(p => p.category))]
  return ['all', ...unique]
})

const filteredProducts = computed(() => {
  return products.filter(product => {

    const matchesSearch =
      product.title.toLowerCase().includes(searchQuery.value.toLowerCase())

    const matchesCategory =
      selectedCategory.value === 'all' ||
      product.category === selectedCategory.value

    return matchesSearch && matchesCategory
  })
})

</script>
