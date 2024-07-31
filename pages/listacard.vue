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
        <div>
            Aggiungi contatti
        </div>
        
        <div>
            <form @submit.prevent="addPerson">
                <input v-model="newNome" required placeholder="inserisci nome">
                <input v-model="newCognome" required placeholder="inserisci cognome"> 
                <input type="number" v-model="newEta" required placeholder="inserisci eta">
                <input v-model="newSesso" required placeholder="inserisci sesso">
                <input v-model="newIndirizzo" required placeholder="inserisci indirizzo">
                <button> add</button>
            </form>
        </div>
    </div>
    <div>
        <div>Lista contatti</div>
        <div>
            <cardcontatti :contatti="contatti" />
        </div>
    </div>
</template>

<style>
</style>
