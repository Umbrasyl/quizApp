<script setup>
import { ref } from 'vue';
import { useRoute } from 'vue-router';
import quizes from "../data/quiz.json";
import Question from '../components/Question.vue';

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
  if (currentQuestion.value < quizLength - 1) {
    currentQuestion.value++;
  } else {
    finished.value = true;
  }
}

function handleCorrect() {
  handleAnswer(true);
}

function handleWrong() {
  handleAnswer(false);
}

</script>


<template>
  <div class="container">
    <div v-if="!finished" class="question">
      <header>
        <h3>{{ `Question ${currentQuestion + 1}/${quizLength}` }}</h3>
        <div class="bar">
          <div :class="`width${currentQuestion}`" class="completion"></div>
        </div>
      </header>
      <Question 
        :question="currentQuiz.questions[currentQuestion]"
        @yes="handleCorrect"
        @no="handleWrong"
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

.question {
  display: flex;
  flex-direction: column;
}

h2 {
  font-size: 2rem;
}

h3 {
  font-size: 1.4rem;
  margin: 1rem 0;
}

.bar {
  width: 15rem;
  height: 2rem;
  background-color: beige;
  margin: 1rem 0;
  border-radius: 0.3rem;
}

.completion {
  height: 100%;
  width: 0%;
  background-color: yellowgreen;
}

.width0 {
  width: 0%;
}

.width1 {
  width: 33%;
}

.width2 {
  width: 66%;
}

</style>