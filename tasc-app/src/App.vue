<script lang="ts" setup>
import { computed, ref } from 'vue';
import TaskForm from './components/TaskForm.vue';
import type { Task } from './type.ts';
import TaskList from './components/TaskList.vue';
const tasks = ref <Task[]>([]);
const message = ref("Tasks App");
const totalDone = computed(() => tasks
.value
.reduce((total, task)=> task.done ? total+1: total, 0));

function handleAddTask(yourTask:string) {   //perchè ho dato al typo tasks questi valori
tasks.value.push({
  id: crypto.randomUUID(),
  title: yourTask,
  done:false
})
}

function toggleDone(id:string) {
  const task = tasks.value.find((task)=> task.id ===id);
if (task) {
  task.done = !task.done;
}
}

function deleteTask (id:string){
  const index = tasks.value.findIndex((task)=> task.id ===id);
  if (index !== -1) {
    tasks.value.splice(index,1);
  }
}
</script>

<template>
  <main>
    <h1>{{ message }}</h1>
    <TaskForm @addTask="handleAddTask"/>
    <h3 v-if="!tasks.length">Add a task to get started.</h3>
    <h3 v-else> {{ totalDone }} /{{ tasks.length }} tasks completed</h3>
    <TaskList :tasks @toggleDone="toggleDone" @removeTask="deleteTask"/>
    <!--<h3>There are {{ tasks.length }}</h3>-->

  </main>
</template>


<style scoped>
main {
  max-width: 800px;
  margin: 1rem auto;
  font-family: cursive;
}
</style>
