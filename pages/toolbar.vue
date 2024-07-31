
<script setup>
import { ref } from 'vue';
import SelectButton from 'primevue/selectbutton';

const but = ref('Piccolo');
const options = ref(['Piccolo', 'Medio', 'Grande', 'Enorme']);
const butColor = ref('Bianco');
const optionsColor = ref(['Bianco', 'Rosso', 'Verde', 'Giallo']);
const butTextBold = ref('Sottile');
const optionsTextBold = ref(['Sottile', 'Grassetto']);
const butTextunder = ref('NonSottolineato');
const optionsTextunder = ref(['NonSottolineato', 'Sottolineato']);
const value = ref('');

function toggleUnder(newValue) {
  butTextunder.value = newValue;
}

function toggleBold(newValue) {
  butTextBold.value = newValue;
}

</script>


<template>
    <div>
      <div class="card flex justify-content-center">
        <div>
          <SelectButton v-model="but" :options="options" aria-labelledby="basic" />
        </div>
        <div>
          <SelectButton v-model="butColor" :options="optionsColor" aria-labelledby="basic" />
        </div>
        <div>
          <SelectButton 
            v-model="butTextBold" 
            :options="optionsTextBold" 
            aria-labelledby="basic" 
            @update:model-value="toggleBold" 
          />
        </div>
        <div>
          <SelectButton 
            v-model="butTextunder" 
            :options="optionsTextunder" 
            aria-labelledby="basic" 
            @update:model-value="toggleUnder" 
          />
        </div>        
      </div>
      <br>
      <p>Hai selezionato questa tipologia per il testo: {{ but }} {{ butColor }} {{ butTextBold }} {{ butTextunder }}</p>
      <br>
      <div>
        <input v-model="value" />
        <br>
        <p>Testo editato</p>
        <p :class="{ 
            grassetto: butTextBold === 'Grassetto', 
            sottolineato: butTextunder === 'Sottolineato',
            rosso: butColor === 'Rosso',
            giallo: butColor === 'Giallo',
            verde: butColor === 'Verde',
            bianco: butColor === 'Bianco',
            piccolo: but === 'Piccolo',
            medio: but === 'Medio',
            grande: but === 'Grande',
            enorme: but === 'Enorme'
            }">{{ value }}</p>
      </div>
    </div>
  </template>
  
  
  <style scoped>
  .grassetto {
    font-weight: bold;
  }
  .sottolineato {
    text-decoration: underline;
  }
  .rosso{
    color: red;
  }
  .giallo{
    color: yellow;
}
  .verde{
    color: green;
}
.bianco{
    color: white;
}
.piccolo{
    font-size: 1rem;
}
.medio{
    font-size: 1.5rem;
}
.grande{
    font-size: 2.5rem;
}
.enorme{
    font-size: 5rem;
}
  </style>
  