<template>
  <MainLayout>
    <h2 class="text-2xl font-semibold mb-6">
      Shopping Cart
    </h2>

    <div v-if="cart.items.length" class="mb-6 flex flex-col md:flex-row gap-4">

      <input
        v-model="searchQuery"
        type="text"
        placeholder="Search in cart..."
        class="border rounded px-4 py-2 w-full md:w-1/2"
      />

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


    <div v-if="cart.items.length">

      <div
        v-for="item in filteredCartItems"
        :key="item.id"
        class="flex justify-between items-center bg-white p-4 rounded shadow mb-4"
      >
        <div>
          <h3 class="font-semibold">{{ item.title }}</h3>
          <p class="text-sm text-gray-500">
            ${{ item.price }} × {{ item.quantity }}
          </p>
        </div>

        <div class="flex items-center gap-4">
          <p class="font-semibold">
            ${{ item.price * item.quantity }}
          </p>

          <button
            @click="cart.removeFromCart(item.id)"
            class="text-red-500 hover:underline"
          >
            Remove
          </button>
        </div>
      </div>

      <div class="text-right mt-6">
        <p class="text-xl font-bold">
          Total: ${{ totalPrice }}
        </p>
      </div>

    </div>

    <div v-else>
      <p class="text-gray-500">Your cart is empty.</p>
    </div>

  </MainLayout>
</template>

<script setup>
import {computed} from 'vue'
import MainLayout from '../layouts/MainLayout.vue'
import {useCartStore} from '../stores/cart'
import {ref} from 'vue'

const cart = useCartStore()

const searchQuery = ref('')
const selectedCategory = ref('all')

const categories = computed(() => {
  const unique = [...new Set(cart.items.map(item => item.category))]
  return ['all', ...unique]
})

const filteredCartItems = computed(() => {
  return cart.items.filter(item => {

    const matchesSearch =
      item.title.toLowerCase().includes(searchQuery.value.toLowerCase())

    const matchesCategory =
      selectedCategory.value === 'all' ||
      item.category === selectedCategory.value

    return matchesSearch && matchesCategory
  })
})


const totalPrice = computed(() =>
  cart.items.reduce((sum, item) => {
    return sum + item.price * item.quantity
  }, 0)
)
</script>
