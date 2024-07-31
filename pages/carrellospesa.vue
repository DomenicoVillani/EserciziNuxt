<script setup>
import { ref } from 'vue';
import { useToast } from 'primevue/usetoast';

const toast = useToast();

let id = 0;
const lista = ref([]);
const oggetto = ref('');

function addTodo() {
    if (oggetto.value.trim() !== '') {
        lista.value.push({ id: id++, text: oggetto.value, done: false, quantita: 0 });
        oggetto.value = '';
    }
}

function RemoveTodo(ogg) {
    lista.value = lista.value.filter(t => t.id !== ogg.id);
}

function addQuantita(ogg) {
    ogg.quantita++;
}

function removeQuantita(ogg) {
    if (ogg.quantita === 0) {
        toast.add({ severity: 'info', summary: 'IMPOSSIBILE', detail: 'IMPOSSIBILE INSERIRE UN NUMERO NEGATIVO', life: 3000 });
    } else {
        ogg.quantita--;
    }
}

function toggleDone(ogg) {
    ogg.done = !ogg.done;
}

</script>

<template>
    <div>
        <div class="flex justify-content-center m-5 text-2xl text-0">
            <h1>Carrello spesa</h1>
        </div>
        <div class="flex justify-content-center">
            <div class="flex flex-column">
                <div class="flex">
                    <FloatLabel>
                        <InputText id="spesa" v-model="oggetto" />
                        <label for="spesa">Oggetto spesa</label>
                    </FloatLabel>
                    <Button label="Aggiungi alla lista della spesa" severity="success" @click="addTodo" class="ml-3" :disabled="oggetto == ''"/>
                </div>
                <div>
                    <ul class="list-none">
                        <li v-for="o in lista" :key="o.id">
                            <Button :icon="o.done ? 'pi pi-check' : 'pi pi-circle'" :class="['mx-2', o.done ? 'p-button-success' : 'p-button-secondary']" @click="toggleDone(o)" />                            
                            <span :class="{ done: o.done }" class="mx-5 text-2xl">{{ o.text }}</span>
                            <Button icon="pi pi-trash" severity="danger" @click="RemoveTodo(o)"/>
                            <span class="mx-5 text-2xl">Quantità: {{ o.quantita }}</span>
                            <Button icon="pi pi-plus" severity="success" @click="addQuantita(o)"/>
                            <Button icon="pi pi-minus" severity="danger" @click="removeQuantita(o)"/>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>
