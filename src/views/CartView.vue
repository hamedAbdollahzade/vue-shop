<template>
  <MainLayout>
    <h2 class="text-2xl font-semibold mb-6">Shopping Cart</h2>

    <!-- Filters -->
    <div v-if="cart.items.length" class="mb-6 flex flex-col md:flex-row gap-4">
      <input
        v-model="searchQuery"
        type="text"
        placeholder="Search in cart..."
        class="border rounded-lg px-4 py-2 w-full md:w-1/2 focus:outline-none focus:ring-2 focus:ring-gray-200"
      />

      <select
        v-model="selectedCategory"
        class="border rounded-lg px-4 py-2 w-full md:w-1/3 focus:outline-none focus:ring-2 focus:ring-gray-200"
      >
        <option v-for="category in categories" :key="category" :value="category">
          {{ category }}
        </option>
      </select>
    </div>

    <!-- Cart Items -->
    <div v-if="cart.items.length">
      <div
        v-if="filteredCartItems.length"
        v-for="item in filteredCartItems"
        :key="item.id"
        class="bg-white p-4 md:p-6 rounded-xl shadow-sm border flex flex-col md:flex-row items-center gap-6 mb-4"
      >
        <!-- Image -->
        <div class="w-28 h-28 flex-shrink-0">
          <img
            :src="item.image"
            :alt="item.title"
            class="w-full h-full object-contain rounded-lg bg-gray-50 p-2"
          />
        </div>

        <!-- Info -->
        <div class="flex-1 text-center md:text-left">
          <h3 class="font-semibold text-lg mb-2">
            {{ item.title }}
          </h3>

          <p class="text-sm text-gray-500 mb-2">
            ${{ formatPrice(item.price) }} × {{ item.quantity }}
          </p>

          <p class="font-bold text-lg">${{ formatPrice(item.price * item.quantity) }}</p>
        </div>

        <!-- Actions -->
        <div class="flex items-center gap-3">
          <button
            @click="cart.decreaseQuantity(item.id)"
            class="w-8 h-8 flex items-center justify-center rounded bg-gray-100 hover:bg-gray-200 transition"
          >
            -
          </button>

          <span class="font-semibold w-6 text-center">
            {{ item.quantity }}
          </span>

          <button
            @click="cart.increaseQuantity(item.id)"
            class="w-8 h-8 flex items-center justify-center rounded bg-gray-100 hover:bg-gray-200 transition"
          >
            +
          </button>

          <button
            @click="cart.removeFromCart(item.id)"
            class="text-red-500 hover:text-red-600 ml-4 text-sm font-medium"
          >
            Remove
          </button>
        </div>
      </div>

      <!-- Empty After Filter -->
      <div v-if="!filteredCartItems.length" class="text-gray-500 text-center mt-6">
        No items match your search.
      </div>

      <!-- Total -->
      <div v-if="filteredCartItems.length" class="text-right mt-8 border-t pt-6">
        <p class="text-xl font-bold">Total: ${{ formatPrice(totalPrice) }}</p>
      </div>
    </div>

    <!-- Completely Empty Cart -->
    <div v-else class="text-center text-gray-500 mt-10">Your cart is empty.</div>
  </MainLayout>
</template>

<script setup>
import { ref, computed } from 'vue'
import MainLayout from '../layouts/MainLayout.vue'
import { useCartStore } from '../stores/cart'

const cart = useCartStore()

const searchQuery = ref('')
const selectedCategory = ref('all')

const categories = computed(() => {
  const unique = [...new Set(cart.items.map((item) => item.category))]
  return ['all', ...unique]
})

const filteredCartItems = computed(() => {
  return cart.items.filter((item) => {
    const matchesSearch = item.title.toLowerCase().includes(searchQuery.value.toLowerCase())

    const matchesCategory =
      selectedCategory.value === 'all' || item.category === selectedCategory.value

    return matchesSearch && matchesCategory
  })
})

const totalPrice = computed(() =>
  cart.items.reduce((sum, item) => {
    return sum + item.price * item.quantity
  }, 0),
)

const formatPrice = (price) => {
  return price.toFixed(2)
}
</script>
