<script setup>

import {ref, computed} from 'vue';

const questions = ref([
  {
    question : 'What is Vuejs?',
    answer : 0,
    options : [
      'A frontend framework',
      'A library',
      'An ice cream maker'
    ],
    selected : null
},
{
    question : 'What is Vuex?',
    answer : 2,
    options : [
      'vue with an  x',
      'A cheese slection',
      'State mangement librarary'
    ],
    selected : null
},
{
    question : 'What is Vue Router used for?',
    answer : 1,
    options : [
      'Walking in space',
      'A routing library for vuejs',
      'Burger sauce',
      'Quizeses'
    ],
    selected : null
},
])

const quizCompleted = ref(false)
const currentQuestion = ref(0)

const score = computed(() => {
  let value = 0
  questions.value.map(q => {
    if(q.selected == q.answer){
      value ++
    }
  })
  return value
})

const getCurrentQuestion = computed(() => {
  let question = questions.value[currentQuestion.value]
  question.index = currentQuestion.value
  return question
})

function SetAnswer(evt) {
  questions.value[currentQuestion.value].selected=evt.target.value;
  evt.target.value=null;
}

const NextQuestion = () => {
  if(currentQuestion.value < questions.value.length){
    currentQuestion.value++
  } else {
    quizCompleted.value = true
  }

}

</script>

<template>
  <main class="app">
    <h1>The Quiz app</h1>
    <section class="quiz">
      <div class="quiz-info">
        <span class="question">{{ getCurrentQuestion.question }}</span>
      </div>
    </section>
  </main>
  
</template>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Montserrat', sans-serif;
}

body {
  background-color:#271C36;
  color: #FFF;

}

</style>
