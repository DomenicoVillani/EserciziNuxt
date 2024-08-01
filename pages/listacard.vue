<script setup>
import { ref } from 'vue';
import cardcontatti from './cardcontatti.vue';

const newNome =ref('')
const newCognome =ref('')
const newEta =ref('')
const newSesso =ref('')
const newIndirizzo =ref('')

const contatti = ref([
    {
    nome: 'domenico',
    cognome: 'villani',
    eta: 24,
    sesso: 'M',
    indirizzo: 'Traversa via assisi Torgiano'
    },
    {
    nome: 'maria',
    cognome: 'rossi',
    eta: 30,
    sesso: 'F',
    indirizzo: 'Via Roma 1, Perugia'
    },
    {
    nome: 'luca',
    cognome: 'bianchi',
    eta: 27,
    sesso: 'M',
    indirizzo: 'Via Milano 2, Torgiano'
    },
    {
    nome: 'laura',
    cognome: 'verdi',
    eta: 22,
    sesso: 'F',
    indirizzo: 'Via Firenze 3, Perugia'
    }
]);

function addPerson(){
    if(newNome.value === '' || newCognome.value === '' || newEta.value === '' || newSesso.value === '' || newIndirizzo.value === '') return
    contatti.value.push({nome:newNome.value , cognome:newCognome.value, eta:newEta.value, sesso:newSesso.value, indirizzo:newIndirizzo.value})
    newNome.value = ''
    newCognome.value = ''
    newEta.value = ''
    newSesso.value = ''
    newIndirizzo.value = ''
}

</script>

<template>
    <div>
        <div class="flex justify-content-center m-6 text-0 text-2xl">
            <h1>Aggiungi contatti</h1>
        </div>
        <div class="flex justify-content-center">
            <FloatLabel>
                <InputText id="nome" v-model="newNome" />
                <label for="nome">Inserisci nome</label>
            </FloatLabel>
            <FloatLabel>
                <InputText id="cognome" v-model="newCognome" />
                <label for="cognome">Inserisci cognome</label>
            </FloatLabel>
            <FloatLabel>
                <InputNumber
                        v-model="newEta"
                        placeholder="inserisci età"
                        :min="1"
                        mode="decimal"
                        class="p-mb-2"
                        id="eta"
                    />
                <label for="eta">Inserisci età</label>
            </FloatLabel>
            <FloatLabel>
                <InputText id="sesso" v-model="newSesso" />
                <label for="sesso">Inserisci sesso</label>
            </FloatLabel>
            <FloatLabel>
                <InputText id="indirizzo" v-model="newIndirizzo" />
                <label for="indirizzo">Inserisci indirizzo</label>
            </FloatLabel>
            <Button label="Aggiungi persona" severity="success" @click="addPerson" class="ml-3" :disabled="oggetto == ''"/>
        </div>
    </div>
    <div>
        <div>
            <cardcontatti :contatti="contatti" />
        </div>
    </div>
</template>

<style>
</style>
