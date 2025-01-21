<template>
  <div>
    <div>
      <p>{{ item.title }}</p>
      <p>{{ item.price * item.quantity }}$</p>
    </div>
    <CounterComponent :basket-index="basketIndex" />
  </div>


</template>



<script setup>
import { computed, inject } from 'vue';
import CounterComponent from './CounterComponent.vue';


const props = defineProps({
  item: Object
})

const basket = inject('basket')

const basketIndex = computed(() => basket.findIndex((el) => el.id === props.item.id))




</script>
