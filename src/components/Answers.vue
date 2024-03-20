<template>
    <div>
      <button v-for="answer in answers" :key="answer.id" @click="selectAnswer(answer.correct)">
        {{ answer.title }}
      </button>
    </div>
  </template>
  
  <script>
  export default {
    props: ['answers'],
    methods: {
      selectAnswer(isCorrect) {
        this.$emit('selectAnswer', isCorrect);
      },
    },
  };
  </script>
  