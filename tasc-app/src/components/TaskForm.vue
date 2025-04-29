<script lang="ts" setup>
import { ref } from 'vue';
const newTask = ref("");

function formSubmitted(){
console.log(newTask)
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