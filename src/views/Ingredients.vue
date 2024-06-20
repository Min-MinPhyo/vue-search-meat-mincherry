<template>

  <div class="p-8">
    <h1 class="text-4xl font-bold mb-4">Ingredients</h1>

    <input
    type="text"
    v-model="keyword"
    class="rounded border-gray-200 w-full mb-3"
    placeholder="Search For Ingredients"
  />


    <router-link 
       :to="{name:'byIngredient',
             params:{ingredient:ingredient.strIngredient},

            }" 
         v-for="ingredient of computedIngredients"
         :key="ingredient.idIngredient" 
     class=" block bg-white rounded p-3 mb-3 shadow"
     >
     <!-- <pre>{{ingredient}}</pre> -->

      <h3 class="text-2xl font-bold mb-2">{{ingredient.strIngredient}}</h3>
      <pre>{{ingredient.strDescription}}</pre>
    </router-link>
  </div>


</template>

<script setup>
import { computed, onMounted,ref } from 'vue';
import axiosClient from '../axiosClient';

const keyword=ref('');
const ingredients=ref([]);

const computedIngredients=computed(()=>{
  if(!computedIngredients) return ingredients;

  return ingredients.value.filter((i)=>{
    // debugger;
    return (i.strDescription || '').toLowerCase().includes(keyword.toLowerCase) ||
    i.strIngredient.toLowerCase().includes(keyword.value.toLowerCase())

  })
  
})

onMounted(()=>{
  axiosClient.get('list.php?i=list')
  .then(({data})=>{
    debugger;
    ingredients.value=data.meals;
  })
})

</script>

<style>

</style>
