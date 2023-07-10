<script setup>
import { RouterLink } from 'vue-router';

const props = defineProps({
  correctAnswers: Number,
  quizLength: Number,
});

</script>


<template>
  <h2>{{ `Your score is ${props.correctAnswers}/${props.quizLength}` }}</h2>
  <RouterLink to="/">Other Quizes</RouterLink>
</template>


<style scoped>

h2 {
  font-size: 2rem;
}

</style>