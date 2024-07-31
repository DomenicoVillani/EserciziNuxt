<script setup>
import { ref } from 'vue';

const loading = ref(false);
const error = ref(null);
const id = ref('');
const pokemonSingolo = ref('');

async function fetchdata() {
    loading.value = true;
    error.value = null;
    console.log('Fetch started');
    try {
        const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${id.value}`);
        console.log('Fetch response received');
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        const data = await response.json();
        console.log('Fetched Data:', data);
        pokemonSingolo.value = data;
        console.log('Pokemon Data:', pokemonSingolo.value);
    } catch (err) {
        console.error('Error fetching data:', err);
        error.value = 'Failed to fetch data: ' + err.message;
    } finally {
        console.log('Fetch process completed');
        loading.value = false;
    }
}
</script>

<template>
    <div>
        <div class="flex justify-content-center m-5">
            <form @submit.prevent="fetchdata">
                <div class="flex justify-content-center">
                    <InputNumber
                        v-model="id"
                        placeholder="Enter Pokémon ID"
                        :min="1"
                        mode="decimal"
                        class="p-mb-2"
                    />
                    <Button label="Cerca" icon="pi pi-search" type="submit" class="p-button p-component p-button-primary" />
                </div>
            </form>
        </div>
        <div class="mt-5">
            <div class="flex justify-content-center"><p v-if="loading"><i class="pi pi-spin pi-spinner text-5xl"></i></p></div>
            <div class="flex justify-content-center"><p v-if="error">{{ error }}</p></div>
            <div v-if="!loading && !error && pokemonSingolo">
                <div class="flex justify-content-center">
                    <Card style="width: 15rem; overflow: hidden" class="mr-5">
                        <template #header>
                            <img alt="Pokemon front" :src="pokemonSingolo.sprites.front_default" style="width: 150px; height: 150px; object-fit: cover;"/>
                        </template>
                        <template #title>{{ pokemonSingolo.name }}</template>
                        <template #subtitle>
                            {{ pokemonSingolo.types[0].type.name }}
                            <span v-if="pokemonSingolo.types[1]"> / {{ pokemonSingolo.types[1].type.name }}</span>
                        </template>
                        <template #content>
                            <p><strong>Height:</strong> {{ pokemonSingolo.height / 10 }} m</p>
                            <p><strong>Weight:</strong> {{ pokemonSingolo.weight / 10 }} kg</p>
                            <p><strong>Abilities:</strong> {{ pokemonSingolo.abilities.map(a => a.ability.name).join(', ') }}</p>
                            <p><strong>Stats:</strong></p>
                            <ul>
                                <li v-for="stat in pokemonSingolo.stats" :key="stat.stat.name">
                                    {{ stat.stat.name }}: {{ stat.base_stat }}
                                </li>
                            </ul>
                        </template>
                    </Card>
                    <Card style="width: 15rem; overflow: hidden">
                        <template #header>
                            <img alt="Pokemon front" :src="pokemonSingolo.sprites.front_shiny" style="width: 150px; height: 150px; object-fit: cover;"/>
                        </template>
                        <template #title>{{ pokemonSingolo.name }}</template>
                        <template #subtitle>
                            {{ pokemonSingolo.types[0].type.name }}
                            <span v-if="pokemonSingolo.types[1]"> / {{ pokemonSingolo.types[1].type.name }}</span>
                        </template>
                        <template #content>
                            <p><strong>Height:</strong> {{ pokemonSingolo.height / 10 }} m</p>
                            <p><strong>Weight:</strong> {{ pokemonSingolo.weight / 10 }} kg</p>
                            <p><strong>Abilities:</strong> {{ pokemonSingolo.abilities.map(a => a.ability.name).join(', ') }}</p>
                            <p><strong>Stats:</strong></p>
                            <ul>
                                <li v-for="stat in pokemonSingolo.stats" :key="stat.stat.name">
                                    {{ stat.stat.name }}: {{ stat.base_stat }}
                                </li>
                            </ul>
                        </template>
                    </Card>
                </div>
            </div>
        </div>
    </div>
</template>

<style>
</style>
