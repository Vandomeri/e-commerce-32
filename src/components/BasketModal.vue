<template>

  <div class="w-full h-full fixed top-0 left-0">

    <div @click="$emit('closeModal')" class="w-full h-full absolute top-0 left-0 bg-[#00000077]"></div>

    <div class="h-full w-1/3 shadow-2xl bg-white relative ml-auto">
      <button @click="$emit('closeModal')" class="absolute right-4 top-4">X</button>
      <h3>Корзина</h3>
      <div v-if="basket.length">
        <p>Список покупок:</p>
        <div>
          <BasketItem v-for="item in basket" :key="item.id" :item="item" />
        </div>
      </div>
      <p v-else>Закажите товары</p>




      <button> <span>30-40 мин</span> <span>Далее</span> <span>{{ overAllSum }}$</span></button>
    </div>



  </div>

</template>

<script setup>
import { computed, inject } from 'vue';
import BasketItem from './BasketItem.vue';



const basket = inject('basket')


const overAllSum = computed(() => basket.reduce((accumulator, currentValue) => accumulator + (currentValue.price * currentValue.quantity), 0))

</script>
