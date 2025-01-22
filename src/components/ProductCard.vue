<template>

  <div class="bg-white rounded-[30px] p-6 shadow-lg">
    <p>{{ title }}</p>
    <p>{{ price }}$</p>
    <p>{{ category }}</p>
    <button v-if="basketIndex === -1" @click="addToCart()"
      class="shadow-lg py-2 px-4 rounded-md text-white bg-yellow-400 mt-4">Купить</button>
    <CounterComponent :basket-index="basketIndex" v-else />
  </div>

</template>

<script setup>
import { computed, inject } from 'vue';
import CounterComponent from './CounterComponent.vue';



const props = defineProps({
  id: String,
  title: String,
  price: Number,
  category: String
})


const basket = inject('basket')

const basketIndex = computed(() => basket.findIndex((item) => item.id === props.id))



function addToCart() {
  basket.push({
    id: props.id,
    title: props.title,
    price: props.price,
    quantity: 1,
  })

}



</script>
