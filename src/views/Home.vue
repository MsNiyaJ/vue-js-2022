<template>
  <AddTask v-show="showAddTask" @add-task="addTask" />
  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script lang="ts">
import Tasks from '../components/Tasks.vue';
import AddTask from '../components/AddTask.vue';
import { defineComponent } from 'vue';

/**
 * @description The list of properties associated with a task.
 * @property {number} id - The ID of the task.
 * @property {string} text - The text of the task.
 * @property {string} day - The day of the task.
 * @property {boolean} completed - Whether the task is completed.
 */
export interface TasksInterface {
  id: number;
  text: string;
  day: string;
  reminder: boolean;
}

export default defineComponent({
  name: 'App',
  props: { showAddTask: Boolean },
  components: {
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [] as TasksInterface[],
    };
  },
  methods: {
    async addTask(task: TasksInterface) {
      const response = await fetch('/api/tasks', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(task),
      });

      const data = await response.json();

      this.tasks = [...this.tasks, data];
      //   this.showAddTask = false;
    },
    async deleteTask(id: number) {
      if (confirm('Are you sure you want to delete this task?')) {
        const response = await fetch(`/api/tasks/${id}`, {
          method: 'DELETE',
        });

        if (response.ok) {
          this.tasks = this.tasks.filter((task) => task.id !== id);
        } else {
          alert('An error occurred while deleting the task.');
        }
      }
    },
    // Update the reminder status of a task
    async toggleReminder(id: number) {
      const taskToToggle = await this.fetchTask(id);
      const updatedTask = {
        ...taskToToggle,
        reminder: !taskToToggle.reminder,
      };

      const response = await fetch(`/api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(updatedTask),
      });

      const data = await response.json();

      // Update the task
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
    },
    // Get all tasks
    async fetchTasks() {
      const response = await fetch('api/tasks');
      const data: TasksInterface[] = await response.json();
      return data;
    },
    // Get a task with the given ID
    async fetchTask(id: number) {
      const response = await fetch(`api/tasks/${id}`);
      const data: TasksInterface = await response.json();
      return data;
    },
  },
  async created() {
    const tasks = await this.fetchTasks();
    this.tasks = tasks;
  },
});
</script>
