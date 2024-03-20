<template>
    <div>
      <Question :title="currentQuestion.title" />
      <Answers :answers="currentQuestion.answers" @selectAnswer="handleAnswer" />
      <button v-if="!isQuizCompleted" @click="nextQuestion">Suivant</button>
      <Results v-if="isQuizCompleted" :score="score" :questions="questions" />
    </div>
  </template>
  
  <script>
  import Question from './Question.vue';
  import Answers from './Answers.vue';
  import Results from './Results.vue';
  import quizData from '../data/halloween.json';

  export default {
    components: { Question, Answers, Results },
    data() {
      return {
        questions: quizData,
        currentQuestionIndex: 0,
        userAnswers: [],
        score: 0,
      };
    },
    computed: {
      currentQuestion() {
        return this.questions[this.currentQuestionIndex];
      },
      isQuizCompleted() {
        return this.currentQuestionIndex >= this.questions.length;
      },
    },
    methods: {
      nextQuestion() {
        if (this.currentQuestionIndex < this.questions.length - 1) {
          this.currentQuestionIndex++;
        }
      },
      handleAnswer(isCorrect) {
        this.userAnswers.push(isCorrect);
        if (isCorrect) {
          this.score++;
        }
        this.nextQuestion();
      },
    },
  };
  </script>
  