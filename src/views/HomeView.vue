<script setup>
import { ref, watch } from "vue";
import q from "../data/quiz.json";
import { RouterLink } from "vue-router";

import Card from "../components/Card.vue";

const quizes = ref(q);
const searchText = ref("");

watch(searchText, () => {
  quizes.value = q.filter((quiz) => { 
    return quiz.name.toLowerCase().includes(searchText.value.toLowerCase());
  });
});
</script>


<template>
  <div class="container">
    <header>
      <h1>Quizes</h1>
      <input v-model.trim="searchText" type="text" placeholder="Search...">
    </header>
    <div class="options-container">
      <RouterLink v-for="quiz in quizes" :key="quiz.id" :to="`/quiz/${quiz.id}`">
        <Card :quiz="quiz" />
      </RouterLink>
    </div>
  </div>
</template>


<style scoped>

.container {
  max-width: 1000px;
  margin: 0 auto;
}

header {
  margin-bottom: 10px;
  margin-top: 30px;
  display: flex;
  align-items: center;
}

header h1 {
  font-weight: bold;
  margin-right: 30px;
}

header input {
  border: none;
  background-color: rgba(128, 128, 128, 0.1);
  padding: 10px;
  border-radius: 5px;
}

.options-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
}

a {
  text-decoration: none;
  color: inherit;
}

</style>