<script lang="ts" setup>
import type { Filter } from '../type.ts';
const props = defineProps<{
    filter: Filter;
    currentFilter: Filter;
}>();
const emits =defineEmits<{
    setFilter: [filter: Filter]
}>();
</script>
<template>
      <button @click="emits('setFilter', props.filter)" class="secondary" :class="{
        contrast: props.currentFilter === props.filter
      }" >{{ props.filter }}</button>
</template>

<style scoped>
button {
    text-transform: capitalize;
}</style>