<template>
  <div class="tasks-container" :key="task.id" v-for="task in tasks">
    <Task
      @toggle-reminder="$emit('toggle-reminder', task.id)"
      @delete-task="$emit('delete-task', task.id)"
      :task="task"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { TasksInterface } from '@/App.vue';
import Task from './Task.vue';

export default defineComponent({
  name: 'Tasks',
  props: {
    tasks: {
      type: Object as () => TasksInterface[],
      default: () => [] as TasksInterface[],
    },
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
