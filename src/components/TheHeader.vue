<template>

  <header class="flex gap-x-5 items-center">
    <div>
      <p>Hello {{ userName }}</p>
      <p>Welcome Back</p>
    </div>

    <div class="max-w-[360px] ml-auto">
      <input class="w-full bg-gray-200 p-4 rounded-lg " type="text" v-model="searchValue" placeholder="Search">
    </div>

    <button class="w-[32px]" @click="showBasket = true"><img src="/images/shopping-cart.png" alt=""></button>
    <BasketModal @closeModal="showBasket = false" v-if="showBasket" />
  </header>

</template>

<script setup>
import { ref } from 'vue';
import BasketModal from './BasketModal.vue';


const userName = ref('John')
const searchValue = ref('')

const showBasket = ref(false)
</script>
