<script setup>

const props = defineProps({
    contatti: Array
});
</script>

<template>
    <h1 class="text">Lista Contatti</h1>
    <div class="grid">
        <div v-for="(contatto, index) in contatti" :key="index" class="col-12 sm:col-6 md:col-3">
            <Card class="card mx-5">
                <template #title>{{ contatto.nome }} {{ contatto.cognome }}</template>
                <template #content>
                    <p class="m-0">Età: {{ contatto.eta }} Sesso: {{ contatto.sesso }}</p>
                    <p class="m-0">Indirizzo: {{ contatto.indirizzo }}</p>
                </template>
            </Card>
        </div>
    </div>
</template>

<style scoped>
.text {
    text-align: center;
    margin-top: 5%;
}
.card {
    padding: 1rem;
    box-sizing: border-box;
}
.card:hover {
    cursor: pointer;
    -webkit-box-shadow: 15px 14px 22px 12px rgba(84, 89, 196, 0.75);
    box-shadow: 15px 14px 22px 12px rgba(93, 99, 214, 0.75);
}
</style>
