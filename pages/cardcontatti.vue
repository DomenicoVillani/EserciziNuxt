<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    contatti: Array
});
</script>

<template>
    <h1 class="text">Lista Contatti</h1>
    <div class="card-div">
        <div v-for="(contatto, index) in contatti" :key="index" class="card">
            <h2>{{ contatto.nome }} {{ contatto.cognome }}</h2>
            <p>Età : {{ contatto.eta }} Sesso: {{ contatto.sesso }}</p>
            <p>Indirizzo: {{ contatto.indirizzo }}</p>
        </div>
    </div>
</template>

<style scoped>
.text{
    text-align: center;
    margin-top: 5%;
}
.card-div{
    display: flex;
    margin: 5%;
    flex-wrap: wrap;
}
.card{
    border: 2px solid white;
    margin: 1%;
    padding: 2%;
}
.card:hover{
    cursor: pointer;
    -webkit-box-shadow: 15px 14px 22px 12px rgba(23,36,255,0.75); 
    box-shadow: 15px 14px 22px 12px rgba(23,36,255,0.75);
}
</style>
