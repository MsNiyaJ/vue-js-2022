<template>
  <button @click="onClick()" :style="{ background: color }" class="btn">
    {{ text }}
  </button>
</template>
<script lang="ts">
export default {
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
      console.log('clicked');
    },
  },
  onClick() {},
};
</script>
<style></style>
