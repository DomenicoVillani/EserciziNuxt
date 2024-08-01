<script setup>

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
  <div class="p-fluid">
    <div class="flex justify-content-center text-0 my-5 text-2xl">
      <h1>Toolbar</h1>
    </div>
    <div class="p-d-flex p-flex-wrap p-jc-center p-mb-4">
      <div class="p-col-12 p-md-6 p-lg-3">
        <div class="card">
          <SelectButton v-model="but" :options="options" aria-labelledby="basic" class="p-mb-3 mb-3 mx-8" />
          <SelectButton v-model="butColor" :options="optionsColor" aria-labelledby="basic" class="p-mb-3 mb-3 mx-8" />
          <SelectButton v-model="butTextBold" :options="optionsTextBold" aria-labelledby="basic" @update:model-value="toggleBold" class="p-mb-3 mb-3 mx-8" />
          <SelectButton v-model="butTextunder" :options="optionsTextunder" aria-labelledby="basic" @update:model-value="toggleUnder" class="p-mb-3 mb-3 mx-8"/>
        </div>
      </div>
      <div class="p-col-12 p-md-6 p-lg-4 p-d-flex p-flex-column p-ai-center">
        <div class="flex flex-column">
          <div class="flex justify-content-center">
            <FloatLabel>
                <InputText id="inputTesto" v-model="value" />
                <label for="inputTesto">Edita il testo</label>
            </FloatLabel>
          </div>
          <div class="flex justify-content-center text-2xl"><p class="p-mb-3">Hai selezionato questa tipologia per il testo: {{ but }} {{ butColor }} {{ butTextBold }} {{ butTextunder }}</p></div>
        </div>
        <div class="flex justify-content-center">
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
.rosso {
  color: red;
}
.giallo {
  color: yellow;
}
.verde {
  color: green;
}
.bianco {
  color: white;
}
.piccolo {
  font-size: 1rem;
}
.medio {
  font-size: 1.5rem;
}
.grande {
  font-size: 2.5rem;
}
.enorme {
  font-size: 5rem;
}
.card {
  padding: 1rem;
}
</style>

  