<template>
    <div>
      <h3>Votre score: {{ score }}/{{ questions.length }}</h3>
      <div v-for="(question, index) in questions" :key="question.id">
        <p>{{ question.title }}</p>
        <p>Réponse choisie: {{ userAnswers[index] ? 'Correcte' : 'Incorrecte' }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['score', 'questions'],
    data() {
      return {
        userAnswers: [], // Ici, tu vas devoir ajuster en fonction de comment tu souhaites afficher les réponses
      };
    },
  };
  </script>
  