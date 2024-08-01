<script setup>

let id = 0;
const todos = ref([]);
const newtodo = ref('');

function addTodo() {
    if (isValidTodo()) {
        todos.value.push({ id: id++, text: newtodo.value.trim(), done: false });
        newtodo.value = '';
    }
}

function removeTodo(todo) {
    todos.value = todos.value.filter((t) => t.id !== todo.id);
}

function toggleTodo(todo) {
    todo.done = !todo.done;
}

function isValidTodo() {
    return newtodo.value.trim().length > 0;
}

const isAddButtonDisabled = computed(() => !isValidTodo());
</script>

<template>
    <div>
        <div class="flex justify-content-center m-6 text-0 text-2xl">
            <h1>TodoList</h1>
        </div>
        <div class="flex justify-content-center">
            <FloatLabel>
                <InputText id="spesa" v-model="newtodo" />
                <label for="spesa">compito da svolgere</label>
            </FloatLabel>
            <Button 
                label="Aggiungi alla todo" 
                severity="success" 
                @click="addTodo" 
                class="ml-3" 
                :disabled="isAddButtonDisabled"
            />
        </div>
        <div class="flex justify-content-center mt-4">
            <div class="card">
                <DataTable :value="todos" tableStyle="min-width: 50rem">
                    <Column header="Spunta">
                        <template #body="{ data }">
                            <Button 
                                icon="pi pi-check"
                                @click="toggleTodo(data)" 
                                class="p-button-text"
                                :class="{ 'p-button-success': data.done, 'p-button-danger': !data.done }"
                            />
                        </template>
                    </Column>
                    <Column header="Azione">
                        <template #body="{ data }">
                            <span :class="{ done: data.done }">{{ data.text }}</span>
                        </template>
                    </Column>
                    <Column header="Rimuovi">
                        <template #body="{ data }">
                            <Button 
                                icon='pi pi-trash'
                                @click="removeTodo(data)" 
                                class="p-button-danger p-button-text"
                            />
                        </template>
                    </Column>
                </DataTable>
            </div>
        </div>
    </div>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>
