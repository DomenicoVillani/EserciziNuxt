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
        <div>
            <h1>Crud</h1>
        </div>

        <div>
            <form @submit.prevent="addTodo">
                <input v-model="newtodo" required placeholder="inserisci in lista">
                <button>add</button>
            </form>
        </div>

        <div>
            <input v-model="searchName" placeholder="ricerca in lista">
        </div>

        <div v-if="editingTodo">
            <h2>Modifica</h2>
            <input v-model="editName" required placeholder="modifica nome">
            <button @click="updateTodo">Aggiorna</button>
            <button @click="editingTodo = null">Annulla</button>
        </div>

        <div>
            <div v-if="search.length === 0 && searchName.length > 0">
                <span>nessun risultato trovato</span>
            </div>
            <div v-else>
                <ul>
                    <li v-for="todo in search" :key="todo.id">
                        <span>{{ todo.nome }}</span>
                        <button @click="startEditing(todo)">Edit</button>
                        <button @click="removeTodo(todo)">Remove</button>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>


<style>
</style>
