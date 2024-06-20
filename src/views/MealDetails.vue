<template>

  <div class="w-[800px] mx-auto">

    <pre>{{ meal }}</pre>

    <h1 class="text-5xl font-bold mb-5">{{ meal.strMeal }}</h1>

    <img :src="meal.strMealThumb" :alt="meal.strMeal" class="max-w-[100%]">


    <div class="grid grid-cols-1 md:grid-cols-3 text-lg py-2">

      <div>
        <strong class="font-bold">
          Category:{{ meal.strCategory }}
        </strong>
      </div>


      <div>
        <strong class="font-bold">
          Area:{{ meal.strArea }}
        </strong>
      </div>



      <div>
        <strong class="font-bold">
          Tags:{{ meal.strTags }}
        </strong>
      </div>


    </div>

    <div class="my-2">
      {{ meal.strInstructions }}
    </div>


    <div class="grid grid-cols-1 sm:grid-cols-2">
      <div>
        <h2 class="grid grid-cols-1 md:grid-cols-2">Ingredient</h2>

        <ul>
          <template v-for="(el, ind) of new Array(20)">
            <li v-if="meal[`strIngredient${ind + 1}`]">
              {{ ind+ 1}} .{{ meal[`strIngredient${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>

      <div>


        <h2 class="grid grid-cols-1 sm:grid-cols-2">Measures</h2>
        <ul>
          <template v-for="(el, ind) of new Array(20)">
            <li v-if="meal[`strMeasure${ind + 1}`]">
              {{ ind+ 1 }} .{{ meal[`strMeasure${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
    </div>

    <div class="mt-4">
      <YouTubeButton :href="meal.strYoutube">Go to youtube</YouTubeButton>

      <!-- <a :href="meal.strSource" target="_blank"
        class="ml-3 px-3 py-2 rounded border-2 text:white border-indigo-600 hover:bg-indigo-800 text-indigo-600">
        View Original Source
      </a> -->

      <a :href="meal.strSource" target="_blank" class="ml-3 px-3 py-2 rounded border-2 text-white-400 hover:bg-indigo-600 transition-colors">View Original Source</a>

    </div>
  </div>

</template>

<script setup>

import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import axiosClient from '../axiosClient.js'
import YouTubeButton from '../components/YouTubeButton.vue';
const route = useRoute()
const meal = ref({})

onMounted(() => {
  axiosClient.get(`lookup.php?i=${route.params.id}`)
    .then(({ data }) => {
      debugger;
      // meal.value = data.meals[0] || {}
      meal.value=data.meals[0] || {}
    })
})


</script>