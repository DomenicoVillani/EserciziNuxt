
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
  const value = ref(0);
  
  function selectOption(index) {
    if (index === questions.value[currentQuestion.value].answer) {
      score.value++;
      value.value+=33
      if(value.value===99){
        value.value++
      }
    }
    currentQuestion.value++;
  }

  const reloadPage = () => {
  window.location.reload();
}
  </script>




<template>
    <div>
      <div class="flex justify-content-center text-0 text-2xl"><h1>Quiz</h1></div>
      <div v-if="currentQuestion < questions.length">
        <div class="flex justify-content-center text-0 text-2xl"><h2>{{ questions[currentQuestion].question }}</h2></div>
        <div class="flex justify-content-center">
          <div v-for="(option, index) in questions[currentQuestion].options" :key="index">
            <Button :label="option" @click="selectOption(index)" class="mr-2 p-5"/>
          </div>
        </div>
      </div>
      <div v-else>
        <div class="flex justify-content-center text-0 text-2xl"><h2>Quiz completato!</h2></div>
        <div class="flex justify-content-center"><p>Hai risposto correttamente a {{ score }} su {{ questions.length }} domande.</p></div>
        <div class="card flex justify-content-center">
            <div class="flex flex-column align-items-center">
              <div>
                  <Knob v-model="value" valueTemplate="{value}%" readonly/>
              </div>
              <div>
                <div class="flex justify-content-center"><p>Vuoi rifare il quiz?</p></div>
                <div class="flex justify-content-center"><Button label="Premi qui" @click="reloadPage()"/></div>
              </div>
            </div>
        </div>
      </div>
    </div>
  </template>
  
  
  
  <style>
  </style>
  