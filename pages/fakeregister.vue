<script setup>
import { ref, computed } from 'vue';

const toast = useToast();
let id = 0;
const users = ref([]);
const newNameUser = ref('');
const newPassUser = ref('');
const visualizzaPass = ref(false);

function addUser() {
    if (isFormValid.value) {
        hasUsers.value = true;
        toast.add({ severity: 'info', summary: 'Notifica', detail: 'Utente aggiunto con successo!', life: 1000 });
        users.value.push({ id: id++, nome: newNameUser.value, pass: newPassUser.value });
        newNameUser.value = '';
        newPassUser.value = '';
    } else {
        alert('Compila tutti i campi correttamente.');
    }
}

const hasUsers = computed(() => users.value.length > 0);

const isFormValid = computed(() => {
    return newNameUser.value !== '' && newPassUser.value.length >= 8;
});
</script>

<template>
    <div class="my-5">
        <div id="app" class="card flex justify-content-center">
        <InputText type="text" v-model="newNameUser" placeholder="inserisci username" class="mr-3"/>
        <Password v-model="newPassUser" toggleMask placeholder="inserisci password " class="mr-3"/>
        <Button label="Aggiungi utente" @click="addUser" :disabled="!isFormValid" class="mr-3"/>
        <Button label="Visualizza tutte le password" @click="visualizzaPass = !visualizzaPass" :disabled="!hasUsers" />
    </div>
    </div>
    <div class="flex justify-content-center">
        <ul class="list-none">
            <li v-for="user in users" :key="user.id" class="my-5">
                <span class="mx-5 text-2xl"><i class="pi pi-user mr-3 text-2xl my-2"></i>Username: {{ user.nome }}</span>
                <br>
                <div v-if="!visualizzaPass">
                    <span class="mx-5 text-2xl"><i class="pi pi-key mr-3 text-2xl"></i>Password: <span v-for="char in user.pass">*</span></span>
                    
                </div>
                <span v-else class="mx-5 text-2xl"><i class="pi pi-key mr-3 text-2xl"></i>Password: {{ user.pass }}</span>
            </li>
        </ul>
    </div>
</template>

<style>
</style>
