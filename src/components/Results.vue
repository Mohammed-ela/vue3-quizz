<template>
    <div>
      <h3>Votre score: {{ score }} sur {{ questions.length }}</h3>
      <ul>
        <li v-for="(question, index) in questions" :key="question.id">
          <p>{{ question.title }}</p>
          <p>
            Votre réponse: {{ userAnswers[index].userAnswer }}
            <span v-if="!userAnswers[index].isCorrect"> (Incorrect)</span>
          </p>
          <p v-if="!userAnswers[index].isCorrect">
            Réponse correcte: {{ userAnswers[index].correctAnswer }}
          </p>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: ['score', 'questions', 'userAnswers'],
  };
  </script>
  