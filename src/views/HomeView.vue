<script setup>
import { ref, onMounted } from "vue";
import Papa from "papaparse";
import HomeSlider from "@/components/HomeSlider.vue";
import HomeGallery from "./HomeGallery.vue";
import ComissionArt from "./ComissionArt.vue";
import HomeVideo from "@/components/HomeVideo.vue";
const csv_url =
  "https://docs.google.com/spreadsheets/d/e/2PACX-1vSx0AOYKCfH0zJV95XbJQmXZAl-1uotT8wuo1MoSQ8CAwZRcBv3inKte83jDMwpfEmCiPz-A2_m0pT4/pub?output=csv";

const data = ref([]);

onMounted(async () => {
  const response = await fetch(csv_url);
  const csv = await response.text();
  Papa.parse(csv, {
    header: true,
    skipEmptyLines: true,
    complete: (result) => {
      console.log(result);
      data.value = result.data;
    },
  });
});
</script>

<template>
  <HomeVideo />
  <HomeSlider />
  <HomeGallery :images="data" />
  <ComissionArt :images="data" />
</template>

<style scoped>
section {
  max-width: 100vw;
  overflow: hidden;
}
</style>
