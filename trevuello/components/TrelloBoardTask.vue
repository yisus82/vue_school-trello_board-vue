<script setup lang="ts">
import type { ID, Task } from '@/types';

const props = defineProps<{ task: Task; }>();

const emit = defineEmits<{ (e: 'delete', payload: ID): void; }>();

const focused = ref(false);

onKeyStroke('Backspace', (e) => {
  if (focused.value) {
    e.preventDefault();
    emit('delete', props.task.id);
  }
});
</script>

<template>
  <div class="task flex gap-2 bg-white p-2 mb-2 rounded shadow-sm w-full max-w-[250px]" @focus="focused = true"
    @blur="focused = false" tabindex="0">
    <DragHandle />
    <span class="title">{{ task.title }}</span>
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

.title {
  overflow-wrap: anywhere;
}

.task:focus,
.task:focus-visible {
  outline: 3px solid gray;
}
</style>