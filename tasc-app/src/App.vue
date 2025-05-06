<script lang="ts" setup>
import { computed, ref } from 'vue';
import TaskForm from './components/TaskForm.vue';
import TaskList from './components/TaskList.vue';
import FilterBtn from './components/FilterBtn.vue';
import type { Task } from './type.ts';
import type { Filter } from './type.ts';
const tasks = ref<Task[]>([]);
const message = ref("Tasks App");
const filter = ref<Filter>("all");
const filterTasks = computed(() => {
  switch (filter.value) {
    case "all":
      return tasks.value;
    case "todo":
      return tasks.value.filter((task) => !task.done);
    case "done":
      return tasks.value.filter((task) => task.done);
  }
  return tasks.value;
});
const totalDone = computed(() => tasks
  .value
  .reduce((total, task) => task.done ? total + 1 : total, 0));

function handleAddTask(yourTask: string) {   //perchè ho dato al typo tasks questi valori
  tasks.value.push({
    id: crypto.randomUUID(),
    title: yourTask,
    done: false
  })
}

function toggleDone(id: string) {
  const task = tasks.value.find((task) => task.id === id);
  if (task) {
    task.done = !task.done;
  }
}

function deleteTask(id: string) {
  const index = tasks.value.findIndex((task) => task.id === id);
  if (index !== -1) {
    tasks.value.splice(index, 1);
  }
}
function setFilter(value: Filter) {
  filter.value = value;
}
</script>

<template>
  <main>
    <h1>{{ message }}</h1>
    <TaskForm @addTask="handleAddTask" />
    <h3 v-if="!tasks.length">Add a task to get started.</h3>
    <h3 v-else> {{ totalDone }} /{{ tasks.length }} tasks completed</h3>
    <div v-if="tasks.length" class="btn-container">
      <FilterBtn :currentFilter="filter" filter="all" @setFilter="setFilter" />
      <FilterBtn :currentFilter="filter" filter="todo" @setFilter="setFilter" />
      <FilterBtn :currentFilter="filter" filter="done" @setFilter="setFilter" />
    </div>
    <TaskList :tasks="filterTasks" @toggleDone="toggleDone" @removeTask="deleteTask" />
    <!--<h3>There are {{ tasks.length }}</h3>-->

  </main>
</template>


<style scoped>
main {
  max-width: 800px;
  margin: 1rem auto;
  font-family: cursive;
}

.btn-container {
  display: flex;
  justify-content: end;
  align-items: center;
  gap: 0.5rem;
  font-size: 10px;
}
</style>
