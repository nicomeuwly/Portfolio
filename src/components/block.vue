<script>
export default {
  name: "Block",
  props: {
    position: Object,
  },
};
</script>

<template>
  <div
    class="block"
    :style="{ left: position.x + 'px', top: position.y + 'px' }"
  >
    🧱
  </div>
</template>

<style scoped>
.block {
  position: absolute;
  font-size: 4rem;
  color: brown;
}
</style>
