<script lang="ts" setup>
import { ref } from 'vue';
const newTask = ref("");
const emit = defineEmits<{addTask: [newTask:string]}> ();

function formSubmitted() {
    if (newTask.value.trim()) {}
    emit ('addTask', newTask.value)
    newTask.value="" //pulisco input dopo l'inserimento
}
</script>
<template>
    <form @submit.prevent="formSubmitted">
        <label for="name">New Task</label>
        <input v-model="newTask" name="newTask" placeholder="Enter your task" />
        <div class="button-container">
            <button>Add</button>
        </div>

    </form>

</template>

<style scoped>
.button-container {
    display: flex;
    justify-content: flex-end;
}

label {
    line-height: 1.9rem;
}

input,
textarea {
    width: 100%;
    padding: 5px;
    outline: none;
    margin: 0;
}

fieldset {
    padding: 20px 40px;
}
</style>