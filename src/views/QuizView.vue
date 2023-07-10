<script setup>
import { ref } from 'vue';
import { useRoute } from 'vue-router';
import quizes from "../data/quiz.json";
import Question from '../components/Question.vue';
import QuestionHeader from '../components/QuestionHeader.vue';

const route = useRoute();
const currentQuiz = quizes.find((quiz) => {
  return quiz.id === parseInt(route.params.id);
});

const quizLength = currentQuiz.questions.length;
const currentQuestion = ref(0);
const finished = ref(false);
let correctAnswers = 0;

function handleAnswer(isCorr) {
  if (isCorr) {
    correctAnswers++;
  }
  currentQuestion.value++;
  if (currentQuestion.value === quizLength) {
    finished.value = true;
  }
}

</script>


<template>
  <div class="container">
    <QuestionHeader
      :current-question="currentQuestion"
      :quiz-length="quizLength"
    />
    <div v-if="!finished">
      <Question 
        :question="currentQuiz.questions[currentQuestion]"
        @answered="handleAnswer"
      />
    </div>
    <div v-else>
      <h2>{{ `Your score is ${correctAnswers}/${quizLength}` }}</h2>
    </div>
  </div>
</template>


<style scoped>

.container {
  padding-top: 5rem;
  padding-left: 14%;
}

h2 {
  font-size: 2rem;
}

</style>