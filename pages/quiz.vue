
<script setup>
  import { ref } from 'vue';
  import Knob from 'primevue/knob';

  
  const questions = ref([
    {
      question: 'Qual è la capitale dell\'Italia?',
      options: ['Roma', 'Milano', 'Napoli'],
      answer: 0
    },
    {
      question: 'Qual è la capitale della Francia?',
      options: ['Parigi', 'Londra', 'Berlino'],
      answer: 0
    },
    {
      question: 'Qual è la capitale della Germania?',
      options: ['Berlino', 'Amburgo', 'Monaco'],
      answer: 0
    }
  ]);
  
  const currentQuestion = ref(0);
  const score = ref(0);
  
  function selectOption(index) {
    if (index === questions.value[currentQuestion.value].answer) {
      score.value++;
    }
    currentQuestion.value++;
  }
  </script>




<template>
    <div>
      <h1>Quiz</h1>
      <div v-if="currentQuestion < questions.length">
        <h2>{{ questions[currentQuestion].question }}</h2>
        <div v-for="(option, index) in questions[currentQuestion].options" :key="index">
          <button @click="selectOption(index)">
            {{ option }}
          </button>
        </div>
      </div>
      <div v-else>
        <h2>Quiz completato!</h2>
        <p>Hai risposto correttamente a {{ score }} su {{ questions.length }} domande.</p>
        <div class="card flex justify-center">
            <div v-if="score===0">
                <Knob v-model="value" valueTemplate="0%" valueColor="SlateGray" rangeColor="MediumTurquoise"/>
            </div>
            <div v-else-if="score===1">
                <Knob v-model="value" valueTemplate="33%" valueColor="SlateGray" rangeColor="MediumTurquoise" readonly/>
            </div>
            <div v-else-if="score===2">
                <Knob v-model="value" valueTemplate="66%" valueColor="SlateGray" rangeColor="MediumTurquoise" readonly/>
            </div>
            <div v-else-if="score===3">
                <Knob v-model="value" valueTemplate="100%" valueColor="SlateGray" rangeColor="MediumTurquoise" readonly/>
            </div>
            
        </div>
      </div>
    </div>
  </template>
  
  
  
  <style>
  </style>
  