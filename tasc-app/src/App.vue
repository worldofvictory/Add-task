<script lang="ts" setup>
import { ref } from 'vue';
import TaskForm from './components/TaskForm.vue';

const message = ref("Tasks App");
</script>

<template>
  <main>
    <h1>{{ message }}</h1>
    <TaskForm />
  </main>
</template>


<style scoped>
main {
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
  margin: 0;
}

fieldset {
  padding: 20px 40px;
}

.button-container {
  display: flex;
  justify-content: flex-end;
}

.btn {
  margin-top: 20px;
  width: 200px;
  height: auto;
}

.ok {
  margin-top: 20px;
  background-color: red;
}
</style>
