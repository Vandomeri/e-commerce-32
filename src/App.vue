<script setup lang="ts">
import { onMounted, provide, reactive, ref } from 'vue';
import CatalogTabs from './components/CatalogTabs.vue';
import TheHeader from './components/TheHeader.vue';

const basket = reactive([])



provide('basket', basket)

const options = {
  debug: false,
};

provide("ol-options", options);

const center = ref([40, 40]);
const projection = ref('EPSG:4326');
const zoom = ref(3);
// const rotation = ref(0);
// const radius = ref(40);
// const strokeWidth = ref(10);
const stroke = ref("#ff0000");
const fill = ref("#ffffff");
const coordinate = ref([40, 40]);
const address = ref('')

function getGeolocation() {
  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition((geo) => {
      center.value = [geo.coords.longitude, geo.coords.latitude]
      coordinate.value = [geo.coords.longitude, geo.coords.latitude]
      zoom.value = 15
      fetch(`https://nominatim.openstreetmap.org/reverse?lat=${geo.coords.latitude}&lon=${geo.coords.longitude}&format=json`)
        .then((resp) => resp.json())
        .then((json) => address.value = `${json.address.city}, ${json.address.road}`)
    })
  }
}

onMounted(() => {
  getGeolocation()
})
</script>

<template>
  <TheHeader :address="address" />

  <CatalogTabs />

  <ol-map :loadTilesWhileAnimating="true" :loadTilesWhileInteracting="true" style="height: 400px">
    <ol-view ref="view" :center="center" :zoom="zoom" :projection="projection" />

    <ol-tile-layer>
      <ol-source-osm />
    </ol-tile-layer>

    <ol-vector-layer>
      <ol-source-vector>
        <ol-feature>
          <ol-geom-point :coordinates="coordinate"></ol-geom-point>
          <ol-style>
            <ol-style-circle :radius="10">
              <ol-style-fill :color="fill"></ol-style-fill>
              <ol-style-stroke :color="stroke" :width="0"></ol-style-stroke>
            </ol-style-circle>
          </ol-style>
        </ol-feature>
      </ol-source-vector>
    </ol-vector-layer>
  </ol-map>
</template>
