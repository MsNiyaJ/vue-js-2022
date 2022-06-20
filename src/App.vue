<!-- Template (HTML) -->
<template>
  <div class="container">
    <Header
      @toggle-add-task="toggleAddTask"
      title="Task Tracker"
      :showAddTask="showAddTask"
    />
    <div v-if="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<!-- Logic (JS) -->
<script lang="ts">
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue';
import AddTask from './components/AddTask.vue';
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
  // List of child compponents
  components: {
    Header,
    Tasks,
    AddTask,
  },
  // List of props
  data() {
    return {
      tasks: [] as TasksInterface[],
      showAddTask: false,
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
      this.showAddTask = false;
    },

    deleteTask(id: number) {
      if (confirm('Are you sure you want to delete this task?')) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    toggleReminder(id: number) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
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

<!-- Style (CSS) -->
<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
