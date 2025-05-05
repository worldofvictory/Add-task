<script lang="ts" setup>
import type { Task } from '../type';
const props = defineProps<{
    tasks: Task[]
}>();
const emits = defineEmits<{
    toggleDone: [id: string];
    removeTask: [id: string];
}>();
</script>
<template>
    <div class="task-list">
        <TransitionGroup name="list" tag="ul">
                <li v-for="task in props.tasks" :key="task.id" class="task">
                    <label>
                        <input @input="emits('toggleDone', task.id)" :checked="task.done" type="checkbox" />
                        <span :class="{ done: task.done }">{{ task.title }} </span>
                    </label>
                    <button @click="emits('removeTask', task.id)" class="outline">Remove</button>
                </li>
        </TransitionGroup>
    </div>
</template>

<style>
.task-list {
    margin-top: 1 rem;
}

.done {
    text-decoration: line-through;
}

.task {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.outline {
    margin-top: 1 rem;

}

.list-enter-active,
.list-leave-active {
    transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
    opacity: 0;
    transform: translateX(30px);
}
</style>