<template>
  <div class="bg-white rounded-lg shadow hover:shadow-lg transition p-4 cursor-pointer">
    <img alt="image" :src="product?.image" class="w-full h-40 object-cover rounded"/>

    <h3 class="mt-3 text-lg font-semibold">
      {{ product?.title }}
    </h3>

    <p class="text-gray-500 mt-1">
      ${{ product?.price }}
    </p>

    <RouterLink
      :to="`/products/${product?.id}`"
      class="inline-block mt-3 text-blue-600 hover:underline"
    >
      View Details
    </RouterLink>
  </div>
</template>

<script setup>
defineProps({
  product: Object
})
</script>
