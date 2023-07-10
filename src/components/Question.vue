<script setup>
import { defineEmits } from 'vue';
const props = defineProps({
  question: {
    id: Number,
    text: String,
    options: Array({
      id: Number,
      label: String,
      text: String,
      isCorrect: Boolean
    }),
  },
});

const emit = defineEmits(["answered"]);

function handleClick(isCorrect) {
  emit("answered", isCorrect);
}

</script>


<template>
  <div class="question">
    <h2>{{ `${props.question.text}?` }}</h2>
    <ul>
      <li v-for="option in props.question.options" :key="option.id">
        <p @click="() => {handleClick(option.isCorrect)}">
          <span class="label">{{ `${option.label}) ` }}</span>{{ option.text }}
        </p>
      </li>
    </ul>
  </div>
</template>


<style scoped>

h2 {
  font-size: 2rem;
  font-weight: bold;
}

ul {
  padding: 0;
}

li {
  list-style: none;
  font-size: 1.6rem;
}

.label {
  font-weight: 600;
}

</style>