<script setup lang="ts">
import type { Column } from '@/types';
import { nanoid } from 'nanoid';
import draggable from 'vuedraggable';

const columns = useLocalStorage<Column[]>('TrelloBoard', [
  {
    id: nanoid(),
    title: 'To Do',
    tasks: [
      { id: nanoid(), title: 'Task 1' },
      { id: nanoid(), title: 'Task 2' },
    ],
  },
  {
    id: nanoid(),
    title: 'In Progress',
    tasks: [
      { id: nanoid(), title: 'Task 3' },
      { id: nanoid(), title: 'Task 4' },
    ],
  },
  {
    id: nanoid(),
    title: 'Done',
    tasks: [
      { id: nanoid(), title: 'Task 5' },
      { id: nanoid(), title: 'Task 6' },
    ],
  },
  {
    id: nanoid(),
    title: 'Archived',
    tasks: [
      { id: nanoid(), title: 'Task 7' },
      { id: nanoid(), title: 'Task 8' },
      { id: nanoid(), title: 'Task 9' },
      { id: nanoid(), title: 'Task 10' }
    ],
  },
]);

const focusNewColumnTitle = () => {
  const title = document.querySelector('.column:last-of-type .title') as HTMLInputElement;
  title.focus();
};

const createColumn = () => {
  const newColumn: Column = {
    id: nanoid(),
    title: '',
    tasks: [],
  };
  columns.value.push(newColumn);
  nextTick(focusNewColumnTitle);
};
</script>

<template>
  <div class="flex items-start gap-4 overflow-x-auto">
    <draggable class="flex gap-4 items-start" v-model="columns" group="columns" item-key="id" :animation="150"
      handle=".drag-handle">
      <template #item="{ element: column }: { element: Column; }">
        <TrelloBoardColumn :column="column" @delete="columns = columns.filter((c) => c.id !== $event)" />
      </template>
    </draggable>
    <button @click="createColumn" class="p-2 bg-gray-200 rounded whitespace-nowrap opacity-50">Add Column</button>
  </div>
</template>
