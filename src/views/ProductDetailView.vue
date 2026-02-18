<template>
  <MainLayout>
    <div v-if="product" class="grid md:grid-cols-2 gap-8">

      <img
        :src="product.image"
        class="w-full h-80 object-cover rounded-lg shadow"
      />

      <div>
        <h2 class="text-3xl font-bold">
          {{ product.title }}
        </h2>

        <p class="text-gray-600 mt-4">
          {{ product.description }}
        </p>

        <p class="text-xl font-semibold mt-6">
          ${{ product.price }}
        </p>

        <button
          class="mt-6 bg-blue-600 text-white px-6 py-2 rounded hover:bg-blue-700 transition"
        >
          Add to Cart
        </button>

        <div class="mt-6">
          <RouterLink
            to="/products"
            class="text-blue-600 "
          >
            ← Back to Products
          </RouterLink>
        </div>
      </div>

    </div>

    <div v-else>
      <p class="text-red-500">Product not found.</p>
    </div>

  </MainLayout>
</template>

<script setup>
import {computed} from 'vue'
import {useRoute} from 'vue-router'
import MainLayout from '../layouts/MainLayout.vue'
import {products} from '../data/products'

const route = useRoute()

const product = computed(() => {
  const id = Number(route.params.id)
  return products.find(p => p.id === id)
})
</script>
