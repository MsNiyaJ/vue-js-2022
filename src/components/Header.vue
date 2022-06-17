<template>
  <header>
    <h1>{{ title }}</h1>
    <Button text="Add Task" color="#5D2C82" />
  </header>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Button from './Button.vue';

export default defineComponent({
  name: 'Header',
  props: {
    title: String,
  },
  components: {
    Button,
  },
});
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
