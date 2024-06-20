<template>

<!-- <input type="text" class="rounded border-2 w-full border-gray-200" placeholder="Search For Meals"> -->

<div class="flex gap-2 mt-3 justify-center">
  <router-link :to="{ name: 'byLetter', params: { letter } }" v-for="letter of letters" :key="letter">
    {{ letter }}
  </router-link>
</div>

<Meals :meals="meals"/>







</template>

<script setup>
import { computed } from '@vue/reactivity';
import { onMounted,watch } from 'vue';
import {useRouter,useRoute} from 'vue-router';
import store from '../store';
import MealItem from '../components/MealItem.vue';
import Meals from "../components/Meals.vue";

const letters = "ABCDEFGHIJKLNOPQRSTUVWHYZ".split("");
const router=useRouter();
const route=useRoute();
const meals=computed(()=>store.state.mealsByLetter);

watch(route,()=>{
  store.dispatch('searchMealsByLetter',route.params.letter)
})

onMounted(()=>{
  store.dispatch('searchMealsByLetter',route.params.letter);
})

</script>

<style>

</style>
