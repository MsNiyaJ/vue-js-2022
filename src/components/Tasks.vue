<template>
  <div class="tasks-container" :key="task.id" v-for="task in (tasks as any)">
    <Task
      @toggle-reminder="$emit('toggle-reminder', task.id)"
      @delete-task="$emit('delete-task', task.id)"
      :task="task"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Task from './Task.vue';

export default defineComponent({
  name: 'Tasks',
  props: {
    tasks: Array,
  },
  components: {
    Task,
  },
  emits: ['delete-task', 'toggle-reminder'],
});
</script>

<style>
.tasks-container {
  margin-top: 1rem;
  margin-bottom: 1rem;
}
</style>
