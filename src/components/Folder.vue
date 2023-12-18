<script>
import { defineProps } from "vue";
export default {
  name: "Folder",
};
</script>

<template>
  <svg width="150px" height="120px">
    <path d="M 0 0 H 50 V 10 H 150 V 30 H 0 V 0" />
    <rect x="0" y="20" width="150px" height="100px" rx="10px" ry="10px" />
  </svg>
</template>

<style scoped>
rect {
  fill: var(--white);
}
path {
  fill: var(--gray-dark);
}
</style>
