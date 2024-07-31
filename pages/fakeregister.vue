<script setup>
import { ref, computed } from 'vue';

let id = 0;
const users = ref([]);
const newNameUser = ref('');
const newPassUser = ref('');
const visualizzaPass = ref(false);

function addUser() {
    users.value.push({ id: id++, nome: newNameUser.value, pass: newPassUser.value });
    newNameUser.value = '';
    newPassUser.value = '';
}

const hasUsers = computed(() => users.value.length > 0);
</script>

<template>
    <div class="my-5">
        <div class="card flex justify-content-center">
            <InputText type="text" v-model="newNameUser" required placeholder="inserisci username" />
            <Password v-model="newPassUser" toggleMask required placeholder="inserisci password "/>
            <Button label="Aggiungi utente" @click="addUser"/>
            <Button label="Visualizza tutte le password" @click="visualizzaPass = !visualizzaPass" :disabled="!hasUsers" />
        </div>
    </div>
    <div class="flex justify-content-center">
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
