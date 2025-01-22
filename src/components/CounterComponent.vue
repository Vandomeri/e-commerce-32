<template>
  <div class="flex items-center gap-x-3">
    <button class="shadow-lg rounded-lg w-8 h-8 flex items-center justify-center" @click="decrement">-</button>
    <span>{{ basket[basketIndex].quantity }}</span>
    <button class="shadow-lg rounded-lg w-8 h-8 flex items-center justify-center" @click="increment">+</button>
  </div>
</template>

<script setup>
import { inject } from 'vue';


const props = defineProps({
  basketIndex: Number
})

const basket = inject('basket')

function decrement() {

  basket[props.basketIndex].quantity--

  if (basket[props.basketIndex].quantity < 1)
    basket.splice(props.basketIndex, 1)
}

function increment() {
  basket[props.basketIndex].quantity++
}

</script>
