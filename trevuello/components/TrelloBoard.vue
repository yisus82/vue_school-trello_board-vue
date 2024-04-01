<script setup lang="ts">
import type { Column } from '@/types';
import { nanoid } from 'nanoid';

const columns = ref<Column[]>([
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
]);
</script>

<template>
  <div class="flex gap-4 overflow-x-auto items-start">
    <div v-for="column in columns" :key="column.id" class="bg-gray-200 p-5 rounded min-w-[250px]">
      <header class="mb-4">
        <h2 class="font-bold">{{ column.title }}</h2>
      </header>
      <TrelloBoardTask v-for="task in column.tasks" :key="task.id" :task="task" />
      <footer>
        <button class="text-gray-500">+ Add Task</button>
      </footer>
    </div>
  </div>
</template>
