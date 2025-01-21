<script setup lang="ts">
import { provide, reactive } from 'vue';
import CatalogTabs from './components/CatalogTabs.vue';
import TheHeader from './components/TheHeader.vue';

const basket = reactive([])



provide('basket', basket)

</script>

<template>
  <TheHeader />

  <CatalogTabs />
</template>
