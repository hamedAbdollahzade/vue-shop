<template>
  <div class="min-h-screen bg-gray-50">

    <header class="bg-white shadow p-4 flex justify-between items-center">
      <h1 class="text-xl font-bold">Vue Shop</h1>
      <div>
        🛒 {{ cart.totalItems || 0 }}
      </div>
    </header>

    <main class="container mx-auto p-6">
      <slot/>
    </main>


  </div>
</template>


<script setup>
import {useCartStore} from '../stores/cart'

const cart = useCartStore()
</script>

