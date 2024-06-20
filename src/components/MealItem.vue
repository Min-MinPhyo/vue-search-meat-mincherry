<template>
<div class="bg-white shadow rouded-xl">
<router-link :to="{name:'mealDetails',params:{id:meal.idMeal}}">
  <img :src="meal.strMealThumb" :alt="strMeal" class="rounded-t-xl w-full h-48 object-cover" />
</router-link>

<div class="p-3">
  <h3 class="font-bold">{{ meal.strMeal }}</h3>
  <p class="mb-4">
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Aliquam, dicta, necessitatibus molestiae impedit
    cupiditate maxime delectus reiciendis aliquid doloribus, aspernatur quo perferendis autem iste esse in et
    ratione repudiandae quasi?

  </p>

  <div class="flex items-center justify-between">
    <YouTubeButton :href="meal.strYoutube">
    Youtube  
    </YouTubeButton>
  </div>
</div>
</div>

</template>

<script setup>
import YouTubeButton from './YouTubeButton.vue';

const {meal}=defineProps({
  meal:{
    required:true,
    type:Object
  }

})


</script>
