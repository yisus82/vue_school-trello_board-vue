<script setup lang="ts">
import type { Column } from '@/types';
import { nanoid } from 'nanoid';
import draggable from 'vuedraggable';

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
</script>

<template>
  <div>
    <draggable class="flex gap-4 overflow-x-auto items-start" v-model="columns" group="columns" item-key="id">
      <template #item="{ element: column }: { element: Column; }">
        <div class="bg-gray-200 p-5 rounded min-w-[250px]">
          <header class="mb-4">
            <h2 class="font-bold">{{ column.title }}</h2>
          </header>
          <TrelloBoardTask v-for="task in column.tasks" :key="task.id" :task="task" />
          <footer>
            <button class="text-gray-500">+ Add Task</button>
          </footer>
        </div>
      </template>
    </draggable>
  </div>
</template>
