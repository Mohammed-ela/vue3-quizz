<template>
    <div>

      <div v-if="!isQuizCompleted">
        <Question :title="currentQuestion.title" />
        <Answers :answers="currentQuestion.answers" @selectAnswer="handleAnswer" />
        <button @click="nextQuestion">Suivant</button>
      </div>
  

      <Results v-else :score="score" :questions="questions" :userAnswers="userAnswers" />
    </div>
  </template>
  
  <script>
  import Question from './Question.vue';
  import Answers from './Answers.vue';
  import Results from './Results.vue';
  import quizData from '../data/halloween.json'; 
  
  export default {
    components: {
      Question,
      Answers,
      Results
    },
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
    
        return this.questions[this.currentQuestionIndex] || null;
      },
      isQuizCompleted() {
     
        return this.currentQuestionIndex >= this.questions.length;
      },
    },
    methods: {
      nextQuestion() {
        this.currentQuestionIndex++;
      },
      handleAnswer(answer, isCorrect) {
        // Enregistre la réponse de l'utilisateur
        this.userAnswers.push({
          userAnswer: answer.title,
          correctAnswer: this.questions[this.currentQuestionIndex].answers.find(a => a.correct).title,
          isCorrect: isCorrect
        });
  
        // Incrémente le score si la réponse est correcte
        if (isCorrect) {
          this.score++;
        }
  
        // Passe à la question suivante ou termine le quiz
        this.nextQuestion();
      },
    },
  };
  </script>
  