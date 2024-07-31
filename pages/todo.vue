<script setup>

import { ref } from 'vue';

let id =0;
const todos = ref([]);
const newtodo = ref('');

function addTodo(){
    todos.value.push({id: id++, text:newtodo.value, done:false})
    newtodo.value = ''
}
function RemoveTodo(todo){
    todos.value= todos.value.filter((t) => t !== todo)
}

</script>
<template>
    <div>
        <div>
            <h1>TodoList</h1>
        </div>
        
        <div>
            <form @submit.prevent="addTodo">
                <input v-model="newtodo" required>
                <button> add</button>
            </form>
        </div>
        <div>
            <ul>
                <li v-for="todo in todos" :key="todo.id">
                    <input type="checkbox" v-model="todo.done">
                    <span :class="{done: todo.done}">{{ todo.text }}</span>
                    <button @click="RemoveTodo(todo)">❌</button>
                </li>
            </ul>
        </div>
    </div>

</template>
  
  <style>
    .done {
        text-decoration: line-through;
    }
  </style>
  