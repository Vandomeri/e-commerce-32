<template>
  <div>
    <button @click="basket[basketIndex].quantity--">-</button>
    <span>{{ basket[basketIndex].quantity }}</span>
    <button @click="basket[basketIndex].quantity++">+</button>
  </div>
</template>

<script setup>
import { inject } from 'vue';


defineProps({
  basketIndex: Number
})

const basket = inject('basket')

</script>
