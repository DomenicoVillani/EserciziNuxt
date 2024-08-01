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
    if(value.value === 0){
        commenti.value.push({ id: id++, stelle: 0, text: text.value });
        text.value = '';
    }
    else{
        commenti.value.push({ id: id++, stelle: value.value, text: text.value });
        text.value = '';
        value.value = 0;
    }
}

</script>

<template>
    <div>
        <div class="flex justify-content-center m-6 text-0 text-2xl"><h1>Star Rating</h1></div>
        <div class="flex flex-column">
            <div class="flex flex-column">
                <div class="flex justify-content-center mb-3">
                    <FloatLabel>
                        <InputText id="spesa" v-model="text" />
                        <label for="spesa">Inserisci commento</label>
                    </FloatLabel>
                </div>
                <div class="flex justify-content-center"><Rating v-model="value" :stars="10"/></div>
                <div class="flex justify-content-center mb-3">
                    <p v-if="value > 0">Hai selezionato {{ value }} stelle</p>
                    <p v-else>Hai selezionato 0 stelle</p>
                </div>
            </div>
            <div class="flex justify-content-center"><Button label="Aggiungi recensione" severity="success" @click="addRec" class="ml-3"/></div>
        </div>
    </div>
    <div>
        <div class="flex justify-content-center text-0 text-2xl">
            <h1>Sezione Commenti</h1>
        </div>
        <div class="flex justify-content-center pb-5">
            <DataTable :value="commenti" tableStyle="width: 50rem">
                <Column field="text" header="Commento"></Column>
                <Column header="Stelle">
                    <template #body="{ data }">
                        <div class="star-rating">
                            <i v-for="n in data.stelle" :key="n" class="pi pi-star-fill"></i>
                            <span class="ml-2">{{ data.stelle }}/10</span>
                        </div>
                    </template>
                </Column>
            </DataTable>
        </div>
    </div>
</template>

<style>
</style>
