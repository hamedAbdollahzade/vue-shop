<template>
  <MainLayout>
    <h2 class="text-2xl font-semibold mb-6">
      Shopping Cart
    </h2>

    <div v-if="cart.items.length">

      <div
        v-for="item in cart.items"
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

const cart = useCartStore()

const totalPrice = computed(() =>
  cart.items.reduce((sum, item) => {
    return sum + item.price * item.quantity
  }, 0)
)
</script>
