<template>
  <div
    @dblclick="$emit('toggle-reminder', task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <h3>
      {{ task.text }}
      <i @click="onDelete(task.id)" class="fas fa-times"></i>
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { TasksInterface } from '@/App.vue';

export default defineComponent({
  name: 'Task',
  props: {
    task: {
      type: Object as () => TasksInterface,
      default: () => ({} as TasksInterface),
    },
  },
  methods: {
    onDelete(id: number) {
      this.$emit('delete-task', id);
    },
  },
});
</script>

<style scope>
.task {
  background-color: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}

.task.reminder {
  border-left: 5px solid green;
}

h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.fas {
  color: red;
  cursor: pointer;
}
</style>
