<template>
  <div class="p-8 pb-0 text-orange-500">
    <h1 class="text-4xl font-bold mb-4">Min Cherry Meals Company</h1>
    <br>
   <br>
  </div>
  <Meals :meals="meals" />
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import store from "../store";
import Meals from "../components/Meals.vue";
import axiosClient from "../axiosClient.js";

const meals = ref([]);

onMounted(async () => {
  for (let i = 0; i < 10; i++) {
    axiosClient
      .get(`random.php`)
      .then(({ data }) => meals.value.push(data.meals[0]));
  }
});
</script>