<template>
  <button @click="onClick()" :style="{ background: color }" class="btn">
    {{ text }}
  </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Button',
  props: {
    text: {
      type: String,
      default: 'Button',
    },
    color: String,
  },
  methods: {
    onClick() {
      this.$emit('toggle-add-task');
    },
  },
});
</script>

<style></style>
