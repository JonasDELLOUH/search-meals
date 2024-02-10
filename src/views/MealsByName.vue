<template>
  <div class="p-8 pb-5">
    <input
      type="text"
      v-model="keyword"
      class="rounded border-2 bg-white border-gray-200 w-full"
      placeholder="Search for Meals"
      @change="search"
    >
  </div>

  <MealList :meals="meals"/>
</template>

<script setup>
import {computed, onMounted, ref} from "vue";
import store from "../store/index.js";
import {searchMeals} from "../store/actions.js";
import {useRoute} from "vue-router";
import MealList from "../components/MealList.vue";

const route = useRoute();
const keyword = ref('');
const meals = computed(() => store.state.searchedMeals);

function search() {
  if (keyword.value) {
    store.dispatch("searchMeals", keyword.value);
  } else {
    store.commit("setSearchedMeals", []);
  }
}

onMounted(() => {
  keyword.value = route.params.name
  if (keyword.value) {
    search()
  }
})
</script>

<style scoped>

</style>