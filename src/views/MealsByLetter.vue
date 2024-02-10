<template>
  <div class="flex gap-2 justify-center mt-2">
    <router-link
      :to="{name: 'byLetter', params: {letter}}"
      v-for="letter of letters"
      :key="letter">
      {{ letter }}
    </router-link>
  </div>

  <MealList :meals="meals"/>
</template>

<script setup>
import {computed, onMounted, watch} from "vue";
import store from "../store/index.js";
import {useRoute} from "vue-router";
import MealList from "../components/MealList.vue";

const route = useRoute();
const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('');
const meals = computed(() => store.state.mealsByLetter)

watch(route, () => {
  store.dispatch('searchMealsByLetter', route.params.letter)
})

onMounted(() => {
  store.dispatch('searchMealsByLetter', route.params.letter)
})
</script>


<style scoped>

</style>