<script setup lang="ts">
import type { Task } from '@/types';
import { nanoid } from 'nanoid';

const emit = defineEmits<{ (e: 'add', payload: Task): void; }>();

const focused = ref(false);
const title = ref('');

const createTask = (e: Event) => {
  e.preventDefault();

  const trimmedTitle = title.value.trim();

  if (!trimmedTitle) {
    return;
  }

  emit('add', { id: nanoid(), title: trimmedTitle } as Task);
  title.value = '';
};
</script>
<template>
  <div>
    <textarea v-model="title" @keydown.tab="createTask" @keydown.enter="createTask" @focus="focused = true"
      @blur="focused = false" :placeholder="focused ? 'Enter a title for the task...' : 'Add a new task...'"
      style="outline: none !important;" :class="{ 'h-10': !focused, 'h-20': focused }"
      class="focus:bg-white focus:shadow resize-none rounded w-full border-none p-2"></textarea>
  </div>
</template>