<script setup lang="ts">
import type { Task } from '@/types';

defineProps<{ task: Task; }>();
</script>

<template>
  <div class="task flex gap-2 bg-white p-2 mb-2 rounded shadow-sm w-full max-w-[250px]">
    <DragHandle />
    <span>{{ task.title }}</span>
  </div>
</template>

<style scoped>
.sortable-drag .task {
  transform: rotate(5deg);
}

.sortable-ghost .task {
  position: relative;
}

.sortable-ghost .task::after {
  content: '';
  @apply absolute top-0 left-0 w-full h-full bg-slate-300 rounded;
}
</style>