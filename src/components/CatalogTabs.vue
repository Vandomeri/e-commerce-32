<template>

  <div class="flex gap-x-5">

    <label class="cursor-pointer" v-for="category in uniqueCategories" :key="category">
      <input type="radio" v-model="activeCategory" hidden :value="category">
      <span>{{ category }}</span>
    </label>

  </div>

  <div class="grid grid-cols-4 gap-8">
    <ProductCard v-for="product in filteredProducts" :key="product.id" :id="product.id" :title="product.title"
      :price="product.price" :category="product.category" />
  </div>


</template>



<script setup>
import { computed, onMounted, ref } from 'vue';
import ProductCard from './ProductCard.vue';

const products = ref([])
const filteredProducts = computed(() => {
  if (activeCategory.value !== '') {
    return products.value.filter((product) => product.category === activeCategory.value)
  }
  return products.value
})
const activeCategory = ref('')

const uniqueCategories = ref()





onMounted(() => {
  fetch('http://localhost:3000/products')
    .then((resp) => resp.json())
    .then((json) => products.value = json)
    .then(() => uniqueCategories.value = [...new Set(products.value.map(product => product.category))])
})



</script>
