<script lang="ts" setup>
import { ref } from 'vue';
import TaskForm from './components/TaskForm.vue';
const tasks = ref <string[]>([]);
const message = ref("Tasks App");
function handleAddTask(yourTask:string) {
tasks.value.push(yourTask)
}
</script>

<template>
  <main>
    <h1>{{ message }}</h1>
    <TaskForm @addTask="handleAddTask"/>
    <ul>
      <li v-for = "(task,index) in tasks" :key="index">  {{ task }}</li>
    </ul>
  </main>
</template>


<style scoped>
main {
  max-width: 800px;
  margin: 1rem auto;
  font-family: cursive;
}
</style>
