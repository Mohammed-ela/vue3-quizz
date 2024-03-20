<template>
    <div>
      <div v-if="!isQuizCompleted">
        <Question :title="currentQuestion.title" />
        <Answers :answers="currentQuestion.answers" @selectAnswer="handleAnswer" />
        <!-- Bouton Précédent : n'est pas affiché pour la première question -->
        <button v-if="currentQuestionIndex > 0" @click="previousQuestion">Précédent</button>
        <!-- Bouton Suivant -->
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
        if (this.currentQuestionIndex < this.questions.length) {
          this.currentQuestionIndex++;
        }
      },
      previousQuestion() {
        if (this.currentQuestionIndex > 0) {
          this.currentQuestionIndex--;
        }
      },
      handleAnswer(answer, isCorrect) {
        // Enregistre ou met à jour la réponse de l'utilisateur pour la question actuelle
        this.userAnswers[this.currentQuestionIndex] = {
          userAnswer: answer.title,
          correctAnswer: this.questions[this.currentQuestionIndex].answers.find(a => a.correct).title,
          isCorrect: isCorrect
        };
  
        // Incrémente le score si la réponse est correcte, ajuste si la réponse est changée
        this.updateScore();
  
        // Passe à la question suivante
        this.nextQuestion();
      },
      updateScore() {
        // Réinitialise le score et le recalcul à partir de userAnswers à chaque réponse
        this.score = this.userAnswers.filter(answer => answer.isCorrect).length;
      },
    },
  };
  </script>
  