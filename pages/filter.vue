<script setup>
import { ref, computed } from 'vue';

let id = 0;
const filtered = ref('');
const list = ref([
    { id: id++, text: 'prova' },
    { id: id++, text: 'saluti' },
    { id: id++, text: 'ciao' }
]);
const newElemList = ref('');

function addElem(){
    list.value.push({id: id++, text:newElemList.value})
    newElemList.value = ''
}

function RemoveElem(elementi) {
    list.value = list.value.filter((t) => t !== elementi);
}

const filteredList = computed(() => {
    if (!filtered.value.trim()) {
        return list.value;
    }
    return list.value.filter((elementi) =>
        elementi.text.toLowerCase().includes(filtered.value.toLowerCase())
    );
});
</script>

<template>
    <div>
        <div>
            <h1>Filter</h1>
        </div>
        
        <div>
            <form @submit.prevent="addElem">
                <input v-model="newElemList" required placeholder="Aggiungi elementi alla lista">
                <button type="submit">Add</button>
            </form>
            <form id="search" @submit.prevent>
                <input name="query" v-model="filtered" placeholder="Ricerca elementi alla lista">
            </form>
        </div>
        <div>
            <ul v-if="filteredList.length">
                <li v-for="elementi in filteredList" :key="elementi.id">
                    <span>{{ elementi.text }}</span>
                    <button @click="RemoveElem(elementi)">❌</button>
                </li>
            </ul>
            <p v-else>La ricerca non ha dato elementi</p>
        </div>
    </div>
</template>

<style>
</style>
