<script setup>
import { ref } from 'vue';
import Rating from 'primevue/rating';
import Button from 'primevue/button';

let id = 0;
const value = ref(0);
const text = ref('');
const commenti = ref([
    { id: id++, stelle: 5, text: 'non mi è piaciuto molto' },
    { id: id++, stelle: 8, text: 'top' }
]);

function addRec() {
    commenti.value.push({ id: id++, stelle: value.value, text: text.value });
    text.value = '';
    value.value = 0;
}

</script>

<template>
    <div>
        <h1>Star Rating</h1>
        <div class="card flex justify-center">
            <form @submit.prevent="addRec">
                <input v-model="text" required placeholder="Inserisci commento">
                <Rating v-model="value" :stars="10" required/>
                <p v-if="value > 0">Hai selezionato {{ value }} stelle</p>
                <p v-else>Hai selezionato 0 stelle</p>
                <button type="submit">Add</button>
            </form>
        </div>
    </div>
    <div>
        <div>
            <h1>Sezione Commenti</h1>
        </div>
        <div>
            <ul>
                <li v-for="commento in commenti" :key="commento.id">
                    <span>Commento: {{ commento.text }}</span>
                    <span> - Stelle selezionate: {{ commento.stelle }}</span>
                </li>
            </ul>
        </div>
    </div>
</template>

<style>
</style>
