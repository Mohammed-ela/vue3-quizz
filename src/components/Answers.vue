<template>
    <div>
      <button v-for="answer in answers" :key="answer.id" @click="selectAnswer(answer)">
        {{ answer.title }}
      </button>
    </div>
  </template>
  
  <script>
  export default {
    props: ['answers'],
    methods: {
      selectAnswer(answer) {
        this.$emit('selectAnswer', answer, answer.correct);
      },
    },
  };
  </script>
  