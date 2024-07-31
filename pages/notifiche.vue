<script setup>
import { ref, onMounted } from 'vue';
import Button from 'primevue/button';
import { useToast } from 'primevue/usetoast';

const toast = useToast();

const valuenotifiche = ref(0);
const valueCarrello = ref(0);
const valuePreferiti = ref(0);

const show = () => {
    toast.add({ severity: 'info', summary: 'Notifica', detail: 'Hai ricevuto una notifica', life: 1000 });
    valuenotifiche.value++;
    sessionStorage.setItem('notificationsCount', valuenotifiche.value.toString());
};
const loadNotificationsCount = () => {
    const savedCount = sessionStorage.getItem('notificationsCount');
    if (savedCount !== null) {
        valuenotifiche.value = parseInt(savedCount, 10);
    } else {
        valuenotifiche.value = 0;
    }
};

const resetNotifiche = () => {
    valuenotifiche.value = 0;
    sessionStorage.setItem('notificationsCount', valuenotifiche.value.toString());
}
onMounted(() => {
    loadNotificationsCount();
});

const aggiungiAlCarrello = () => {
    toast.add({ severity: 'info', summary: 'Carrello', detail: 'Prodotto aggiunto al carrello', life: 1000 });
    valueCarrello.value++;
}

const resetCarrello = () => {
    valueCarrello.value = 0;
    toast.add({ severity: 'error', summary: 'Carrello', detail: 'Carrello resettato', life: 3000 });
}

const aggiungiPreferiti = () => {
    toast.add({ severity: 'info', summary: 'Carrello', detail: 'Prodotto aggiunto al carrello', life: 1000 });
    valuePreferiti.value++;
}

const resetPreferiti = () => {
    valuePreferiti.value = 0;
    toast.add({ severity: 'error', summary: 'Preferiti', detail: 'Preferiti resettati', life: 3000 });
}

</script>

<template>
    <div class="flex justify-content-between flex-wrap m-8">
        <div>
            <Button label="Inviami una notifica" @click="show" />
        </div>
        <div> 
            <div class="flex flex-column align-items-center">
                <div v-if="valuenotifiche">
                    <Avatar v-badge.danger="valuenotifiche" icon="pi pi-user" size="xlarge" />
                </div>
                <div v-else>
                    <Avatar icon="pi pi-user" size="xlarge"/>
                </div>
                <Button label="Reset notifiche" @click="resetNotifiche" :disabled="valuenotifiche <= 0" class="mt-3"/>
            </div>
        </div>
    </div>
    <div class="p-5 flex justify-content-between">
        <div class="flex justify-content-start">
            <Card style="width: 20rem; overflow: hidden" class="mr-5">
                <template #header>
                    <img alt="user header" src="https://media.gqitalia.it/photos/643d3a6d19feea02f597ff1a/master/w_1600%2Cc_limit/Samsung%2520Galaxy%2520A54.jpg" width="300"/>
                </template>
                <template #title>Telefono Samasung</template>
                <template #subtitle>Samsung</template>
                <template #content>
                    <p class="m-0">
                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Inventore sed consequuntur error repudiandae numquam deserunt quisquam repellat libero asperiores earum nam nobis, culpa ratione quam perferendis esse, cupiditate neque
                        quas!
                    </p>
                </template>
                <template #footer>
                    <div class="flex gap-3 mt-1">
                        <Button label="Aggiungi ai preferiti" severity="secondary" outlined class="w-full" @click="aggiungiPreferiti"/>
                        <Button label="Aggiungi al carrello" class="w-full" @click="aggiungiAlCarrello"/>
                    </div>
                </template>
            </Card>
            <Card style="width: 20rem; overflow: hidden" class="mr-5">
                <template #header>
                    <img alt="user header" src="https://centronoli-bucket.s3.eu-west-3.amazonaws.com/wp-content/uploads/2023/09/19232905/iphone-12-green-select-2020.png" width="250"/>
                </template>
                <template #title>Telefono Iphone</template>
                <template #subtitle>Iphone</template>
                <template #content>
                    <p class="m-0">
                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Inventore sed consequuntur error repudiandae numquam deserunt quisquam repellat libero asperiores earum nam nobis, culpa ratione quam perferendis esse, cupiditate neque
                        quas!
                    </p>
                </template>
                <template #footer>
                    <div class="flex gap-3 mt-1">
                        <Button label="Aggiungi ai preferiti" severity="secondary" outlined class="w-full" @click="aggiungiPreferiti" />
                        <Button label="Aggiungi al carrello" class="w-full" @click="aggiungiAlCarrello"/>
                    </div>
                </template>
            </Card>
            <Card style="width: 20rem; overflow: hidden" class="mr-5">
                <template #header>
                    <img alt="user header" src="https://i.ebayimg.com/images/g/pFkAAOSwnupktCu1/s-l1200.webp" width="300"/>
                </template>
                <template #title>Telefono Vecchio stile</template>
                <template #subtitle>Vecchio stile</template>
                <template #content>
                    <p class="m-0">
                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Inventore sed consequuntur error repudiandae numquam deserunt quisquam repellat libero asperiores earum nam nobis, culpa ratione quam perferendis esse, cupiditate neque
                        quas!
                    </p>
                </template>
                <template #footer>
                    <div class="flex gap-3 mt-1">
                        <Button label="Aggiungi ai preferiti" severity="secondary" outlined class="w-full" @click="aggiungiPreferiti" />
                        <Button label="Aggiungi al carrello" class="w-full" @click="aggiungiAlCarrello"/>
                    </div>
                </template>
            </Card>
        </div>
        <div class="flex justify-content-between">
            <div class="mr-8"> 
                <div class="flex flex-column align-items-center">
                    <div v-if="valuePreferiti">
                        <Avatar v-badge.danger="valuePreferiti" icon="pi pi-bookmark-fill" size="xlarge" />
                    </div>
                    <div v-else>
                        <Avatar icon="pi pi-bookmark-fill" size="xlarge"/>
                    </div>
                    <Button label="Reset preferiti" @click="resetPreferiti" :disabled="valuePreferiti <= 0" class="mt-3"/>
                </div>
            </div>
            <div> 
                <div class="flex flex-column align-items-center">
                    <div v-if="valueCarrello">
                        <Avatar v-badge.danger="valueCarrello" icon="pi pi-shopping-cart" size="xlarge" />
                    </div>
                    <div v-else>
                        <Avatar icon="pi pi-shopping-cart" size="xlarge"/>
                    </div>
                    <Button label="Reset carrello" @click="resetCarrello" :disabled="valueCarrello <= 0" class="mt-3"/>
                </div>
            </div>
        </div>
    </div>

</template>

<style scoped>

</style>
