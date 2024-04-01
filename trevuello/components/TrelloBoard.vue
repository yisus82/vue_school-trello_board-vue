<script setup lang="ts">
import type { Column, Task } from '@/types';
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

const altKeyPressed = useKeyModifier('Alt');
</script>

<template>
  <div>
    <draggable class="flex gap-4 overflow-x-auto items-start" v-model="columns" group="columns" item-key="id"
      :animation="150" handle=".drag-handle">
      <template #item="{ element: column }: { element: Column; }">
        <div class="bg-gray-200 p-5 rounded min-w-[250px]">
          <header class="flex gap-2 mb-4">
            <DragHandle />
            <h2 class="font-bold">{{ column.title }}</h2>
          </header>
          <draggable v-model="column.tasks" :group="{ name: 'tasks', pull: altKeyPressed ? 'clone' : true }"
            item-key="id" :animation="150" handle=".drag-handle">
            <template #item="{ element: task }: { element: Task; }">
              <div>
                <TrelloBoardTask :task="task" />
              </div>
            </template>
          </draggable>
          <footer>
            <NewTask @add="column.tasks.push($event)" />
          </footer>
        </div>
      </template>
    </draggable>
  </div>
</template>
