<script setup lang="ts">
import type { Column, ID, Task } from '@/types';
import draggable from 'vuedraggable';

const props = defineProps<{ column: Column; }>();

const emit = defineEmits<{ (e: 'delete', payload: ID): void; }>();

const altKeyPressed = useKeyModifier('Alt');

const blurTitle = (e: Event) => {
  const target = e.target as HTMLInputElement;
  if (target.value.trim() === '') {
    target.focus();
    return;
  }
  target.blur();
};

const focused = ref(false);

onKeyStroke('Backspace', (e) => {
  if (focused.value) {
    e.preventDefault();
    emit('delete', props.column.id);
  }
});
</script>

<template>
  <div class="column bg-gray-200 p-5 rounded min-w-[250px]" @focus="focused = true" @blur="focused = false"
    tabindex="0">
    <header class="flex gap-2 mb-4">
      <DragHandle />
      <input type="text" class="title bg-transparent focus:bg-white rounded px-1 w-4/5 text-xl font-bold"
        v-model="column.title" @keydown.enter="blurTitle" @keydown.escape="blurTitle" @keydown.tab="blurTitle"
        @blur="blurTitle" />
    </header>
    <draggable v-model="column.tasks" :group="{ name: 'tasks', pull: altKeyPressed ? 'clone' : true }" item-key="id"
      :animation="150" handle=".drag-handle">
      <template #item="{ element: task }: { element: Task; }">
        <div>
          <TrelloBoardTask :task="task" @delete="column.tasks = column.tasks.filter((t) => t.id !== $event)" />
        </div>
      </template>
    </draggable>
    <footer>
      <NewTask @add="column.tasks.push($event)" />
    </footer>
  </div>
</template>

<style scoped>
.title:focus,
.title:focus-visible {
  outline: 3px solid gray;
}

.column:focus,
.column:focus-visible {
  border: 5px solid gray;
  outline: none;
}
</style>