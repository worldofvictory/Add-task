<script lang="ts" setup>
import {ref} from 'vue';
const message = ref("Tasks App");
const newTask = ref("");
const addTask = ref("")
</script>

<template>
  <main>
  <h1>{{message}}</h1>
  <form>
    <div class="form-control">
          <label for="name">New Task</label>
          <input v-model ="newTask" name="newTask"  placeholder="Enter your task" />   
          <button @click="addTask">add</button>
    </div>
  </form>
  <p class="">{{ newTask }}</p>
</main>
</template>

<style scoped>
main{
  max-width: 800px;
  margin: 1rem auto;
  font-family: cursive;
}

label {
    line-height: 1.9rem;
  }
  input,
    textarea {
    width: 100%;
    padding: 5px;
    outline: none;
  }
  fieldset {
   padding: 20px 40px;
 }
</style>
