<script setup lang="ts">
import type { Task } from '@/types';

defineProps<{ task: Task; }>();
</script>

<template>
  <div class="flex gap-2 bg-white p-2 mb-2 rounded shadow-sm w-full max-w-[250px]">
    <DragHandle />
    <span>{{ task.title }}</span>
  </div>
</template>