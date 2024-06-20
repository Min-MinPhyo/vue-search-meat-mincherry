<template>
  <div>
    <div class="p-8 pb-0">
      <input
        type="text"
        v-model="keyword"
        class="rounded border-gray-200 w-full"
        placeholder="Search For Meals"
        @change="searchMeals()"
      />
    </div>

    <!-- <div class="grid grid-cols-1 md:grid-cols-3 gap-3 p-8">
      <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal"></MealItem>
      <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal"></MealItem>
    </div> -->
  </div>

  <!-- <pre>{{meals}}</pre> -->
  <Meals :meals="meals"/>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../axiosClient.js";
import YouTubeButton from "../components/YouTubeButton.vue";
import store from "../store";
// import MealItem from '../components/MealItem.vue.js';
import MealItem from "../components/MealItem.vue";
import Meals from  "../components/Meals.vue";

const route = useRoute();
const keyword = ref("");
const meals = computed(() => store.state.searchedMeals);

function searchMeals() {
  if(keyword.value){
    store.dispatch("searchMeals", keyword.value);
  }else{
    store.commit('searchMeals',keyword.value);
  }
 
}

onMounted(() => {
  keyword.value = route.params.name;
  if (keyword.value) {
    searchMeals();
  }
});
</script>

<style></style>
