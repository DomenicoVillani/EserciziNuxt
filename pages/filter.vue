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
        <div class="flex justify-content-center m-5 text-2xl text-0">
            <h1>Filter</h1>
        </div>
        <div class="flex flex-column">
            <div class="flex justify-content-center">
                <FloatLabel>
                    <InputText id="elemento" v-model="newElemList" />
                    <label for="elemento">Aggiungi elementi alla lista</label>
                </FloatLabel>
                <Button label="Aggiungi" severity="success" @click="addElem" class="ml-3" :disabled="oggetto == ''"/>
            </div>
            <div class="flex justify-content-center mt-5">
                <FloatLabel>
                    <InputText id="elemento" v-model="filtered" />
                    <label for="elemento">Cerca nella lista</label>
                </FloatLabel>
            </div>
        </div>
        <div class="flex justify-content-center">
            <ul v-if="filteredList.length" class="list-none">
                <li v-for="elementi in filteredList" :key="elementi.id"  class="mt-3" >
                    <span class="mx-5 text-2xl">{{ elementi.text }}</span>
                    <Button @click="RemoveElem(elementi)" label="Rimuovi"/>
                </li>
            </ul>
            <p v-else class="text-2xl">La ricerca non ha dato elementi</p>
        </div>
    </div>
</template>

<style>
</style>
