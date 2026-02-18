<template>
  <div class="min-h-screen bg-gray-50">

    <header class="bg-white shadow p-4 flex justify-between items-center">
      <RouterLink to="/products" class="text-xl font-bold">
        Vue Shop
      </RouterLink>

      <RouterLink to="/cart" class="relative">
        🛒 {{ cart.totalItems }}
      </RouterLink>
    </header>


    <main class="container mx-auto p-6">
      <slot/>
    </main>


  </div>
</template>


<script setup>
import {useCartStore} from '../stores/cart'
import {RouterLink} from 'vue-router'

const cart = useCartStore()
</script>

