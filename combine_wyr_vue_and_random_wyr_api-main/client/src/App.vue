<script setup>

import { ref, onMounted } from 'vue'

import WouldYouRather from './components/WouldYouRather.vue'
import wyrService from './services/wyrService';

const wyrQuestion = ref('')
const wyrAnswer1 = ref('')
const wyrAnswer2 = ref('')

onMounted( () => {
  wyrService.getRandomWYR().then( wyrData => {
    wyrQuestion.value = wyrData.question 
    wyrAnswer1.value = wyrData.answer1 
    wyrAnswer2.value = wyrData.answer2
  })
})

// Will store the user's selection, either 'Triangle house' or 'Circle house'
const userSelection = ref('')

function updateUserSelection(userChoice) {
  userSelection.value = `Thanks! You chose ${userChoice}`
}

</script>

<template>

<div id="app">
  <h1>Hello! Would You Rather...</h1>

  <WouldYouRather 
    v-bind:question="wyrQuestion" 
    v-bind:answer1="wyrAnswer1" 
    v-bind:answer2="wyrAnswer2"
    v-on:answer-selected="updateUserSelection">
  </WouldYouRather>

  {{  userSelection }}

</div>

</template>

<style scoped>

#app {
  background-color: aqua;
}

</style>





