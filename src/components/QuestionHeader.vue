<script setup>

const props = defineProps({
  currentQuestion: Number,
  quizLength: Number,
});

</script>


<template>
  <header>
    <h3>{{ `Question ${props.currentQuestion}/${props.quizLength}` }}</h3>
    <div class="bar">
      <div 
        :style="{width: `${props.currentQuestion/props.quizLength * 100}%`}" 
        class="completion"
      ></div>
    </div>
  </header>
</template>


<style scoped>

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
  transition: width 0.5s ease;
  background-color: yellowgreen;
}

</style>