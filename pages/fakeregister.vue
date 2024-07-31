<script setup>

import { ref } from 'vue';

let id =0;
const users = ref([]);
const newNameUser = ref('');
const newPassUser = ref('');
const visualizzaPass = ref(false);

function addUser(){
    users.value.push({id: id++, nome:newNameUser.value, pass:newPassUser.value})
    newNameUser.value = ''
    newPassUser.value = ''
}
</script>
<template>
        <div>
            <form @submit.prevent="addUser">
                <input v-model="newNameUser" required placeholder="inserisci username">
                <input type="password" v-model="newPassUser" required minlength="8" placeholder="ins password almeno 8 caratteri">
                <button> add</button>
            </form>
            <button @click="visualizzaPass= !visualizzaPass">Vedi tutte le password</button>
        </div>
        <div>
            <ul>
                <li v-for="user in users" :key="user.id">
                    <span>USERNAME: {{ user.nome }}</span>
                    <br>
                    <div v-if="!visualizzaPass">
                        <span>Password: </span>
                        <span v-for="char in user.pass">*</span>
                    </div>
                    <span v-else>Password: {{ user.pass }}</span>
                </li>
            </ul>
        </div>
</template>
<style>

</style>