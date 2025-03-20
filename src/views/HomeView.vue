<script setup>
import { ref, onMounted } from "vue";
import Papa from "papaparse";
import HomeSlider from "@/components/HomeSlider.vue";
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
  <HomeSlider />
  <section>
    <pre>  {{ data }}</pre>
  </section>
</template>

<style scoped></style>
