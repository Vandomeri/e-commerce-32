<template>

  <header class="flex gap-x-5 items-center">
    <div>
      <p>Hello {{ userName }}</p>
      <p>Welcome Back</p>
      <p>{{ address }}</p>
    </div>

    <div class="max-w-[360px] ml-auto">
      <input class="w-full bg-gray-200 p-4 rounded-lg " type="text" v-model="searchValue" placeholder="Search">
    </div>

    <button class="w-[32px] relative" @click="showBasket = true">
      <img src="/images/shopping-cart.png" alt="">
      <div class="w-4 h-4 rounded-full bg-red-500 text-white absolute -top-2 -right-2 text-xs" v-if="productsCount">{{
        productsCount }}</div>
    </button>
    <BasketModal @closeModal="showBasket = false" v-if="showBasket" />
  </header>

</template>

<script setup>

defineProps({
  address: String
})

import { computed, inject, ref } from 'vue';
import BasketModal from './BasketModal.vue';

const basket = inject('basket')

const productsCount = computed(() => {
  if (basket.length) {
    return basket.reduce((acc, curr) => acc + curr.quantity, 0)
  }
  return 0
})

const userName = ref('John')
const searchValue = ref('')

const showBasket = ref(false)
</script>
