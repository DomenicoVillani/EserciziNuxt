<script setup>
import { ref } from 'vue';

const pokemonList = ref([]);
const loading = ref(false);
const error = ref(null);

const api_url = 'https://pokeapi.co/api/v2/pokemon?limit=15';

async function fetchdata(){
    loading.value = true;
    error.value = null;
    console.log('Fetch started');
    try {
        const response = await fetch(api_url);
        console.log('Fetch response received');
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        const data = await response.json();
        console.log('Fetched Data:', data);
        pokemonList.value = data.results; 
        console.log('Pokemon List:', pokemonList.value); 
    } catch (err) {
        console.error('Error fetching data:', err);
        error.value = 'Failed to fetch data: ' + err.message;
    } finally {
        console.log('Fetch process completed');
        loading.value = false;
    }
}
fetchdata()
</script>

<template>
    <div class="container">
        <p v-if="loading">Loading...</p>
        <p v-if="error">{{ error }}</p>
        <div v-if="!loading && !error && pokemonList.length > 0" class="pokemon-grid">
            <div class="card" v-for="pokemon in pokemonList" :key="pokemon.name">
                <div class="card-header">
                    <h1>{{ pokemon.name }}</h1>
                </div>
                <div class="card-body">
                    <a :href="pokemon.url" target="_blank" title="Click to view more details">{{ pokemon.url }}</a>
                </div>
            </div>
        </div>
    </div>
</template>


<style scoped>
.container {
    padding: 20px;
}

.pokemon-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr); 
    gap: 20px;
}

.card {
    border: 1px solid #ddd;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    padding: 16px;
    background-color: #fff;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    min-height: 250px; /* Altezza minima per le card */
    overflow: hidden; /* Nascondi il contenuto in eccesso */
}

.card-header {
    font-size: 1.5rem;
    font-weight: bold;
    margin-bottom: 10px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}

.card-body {
    font-size: 1rem;
    color: #555;
    overflow: hidden; /* Nascondi il testo in eccesso */
    text-overflow: ellipsis; /* Aggiungi ellipsis al testo in eccesso */
    white-space: normal; /* Permetti il testo a capo */
    max-height: 150px; /* Altezza massima per la sezione del testo */
}

.card-body a {
    display: block;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: normal; /* Permetti il testo a capo */
    color: #007bff; /* Colore link */
    text-decoration: none; /* Rimuovi sottolineatura dal link */
}

.card-body a:hover {
    text-decoration: underline; /* Sottolinea il link al passaggio del mouse */
}
</style>



