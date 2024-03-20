<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>
<template>
  <div id="app">
    <Quizz />
  </div>
</template>

<script>
import Quizz from './components/Quizz.vue';

export default {
  name: 'App',
  components: {
    Quizz
  }
};
</script>
