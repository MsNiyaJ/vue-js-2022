<!-- Template (HTML) -->
<template>
  <div class="container">
    <Header title="Task Tracker" />
  </div>
</template>

<!-- Logic (JS) -->
<script lang="ts">
import Header from './components/Header.vue';
import { defineComponent } from 'vue';

/**
 * @description The list of properties associated with a task.
 * @property {number} id - The ID of the task.
 * @property {string} text - The text of the task.
 * @property {string} day - The day of the task.
 * @property {boolean} completed - Whether the task is completed.
 */
interface TasksInterface {
  id: number;
  text: string;
  day: string;
  completed: boolean;
}

export default defineComponent({
  name: 'App',
  // List of child compponents
  components: {
    Header,
  },
  // List of props
  data() {
    return {
      tasks: [] as TasksInterface[],
    };
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Learn Vue',
        day: 'March 1st at 2:30PM',
        completed: false,
      },
      {
        id: 2,
        text: 'Doctors Appointment',
        day: 'March 3rd at 2:30PM',
        completed: false,
      },
      {
        id: 3,
        text: 'Food Shopping',
        day: 'March 12st at 1:30PM',
        completed: false,
      },
    ];
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
