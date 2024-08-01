<script setup>
import { computed, ref } from 'vue';

let id = 0;
const todos = ref([]);
const newtodo = ref('');
const searchName = ref('');
const editingTodo = ref(null);
const editName = ref(''); 
function addTodo() {
    if (newtodo.value.trim() === '') return;
    todos.value.push({ id: id++, nome: newtodo.value });
    newtodo.value = ''; 
}
function removeTodo(todo) {
    todos.value = todos.value.filter(t => t.id !== todo.id);
}

function startEditing(todo) {
    editingTodo.value = todo;
    editName.value = todo.nome;
}

function updateTodo() {
    if (editName.value.trim() === '') return;
    const todo = editingTodo.value;
    todo.nome = editName.value;
    editingTodo.value = null; 
    editName.value = ''; 
}

const search = computed(() => {
    return todos.value.filter(todo =>
        todo.nome.toLowerCase().startsWith(searchName.value.toLowerCase())
    );
});
</script>


<template>
    <div>
        <div class="flex justify-content-center m-6 text-0 text-2xl">
            <h1>Crud</h1>
        </div>
        <div class="flex flex-column">
            <div class="flex flex-column">
                <div class="flex justify-content-center">
                    <FloatLabel>
                        <InputText id="listaCrud" v-model="newtodo" />
                        <label for="listaCrud">Inserisci nella lista</label>
                    </FloatLabel>
                    <Button label="Aggiungi alla lista" severity="success" @click="addTodo" class="ml-3"/>
                </div>
                <div class="flex justify-content-center mt-5">
                    <FloatLabel>
                        <InputText id="Ricerca" v-model="searchName" />
                        <label for="Ricerca">Ricerca nella lista</label>
                    </FloatLabel>
                </div>
            </div>
    
            <div v-if="editingTodo" class="flex flex-column">
                <div class="flex justify-content-center text-0 text-2xl"><h2>Modifica</h2></div>
                <div>
                    <div class="flex justify-content-center">
                        <FloatLabel>
                            <InputText id="Modifica" v-model="editName" />
                            <label for="Modifica">Modifica elemento</label>
                        </FloatLabel>
                    </div>
                    <div class="flex justify-content-center mt-5">
                        <Button label="Aggiorna" severity="success"  @click="updateTodo" class="ml-3"/>
                        <Button label="Annulla" severity="danger" @click="editingTodo = null" class="ml-3"/>
                    </div>
                </div>
            </div>
    
            <div class="flex justify-content-center">
                <div v-if="search.length === 0 && searchName.length > 0">
                    <span class="text-0 text-2xl">nessun risultato trovato</span>
                </div>
                <div v-else>
                    <ul class="list-none">
                        <li v-for="todo in search" :key="todo.id">
                            <span class="text-0 text-2xl">{{ todo.nome }}</span>
                            <Button @click="startEditing(todo)" icon="pi pi-pencil"/>
                            <Button @click="removeTodo(todo)" icon="pi pi-trash"/>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>


<style>
</style>
