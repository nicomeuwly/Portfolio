<script>
export default {
  name: "Window",
  methods: {
    closeWindow() {
      this.$emit("child-to-parent", false);
    },
  },
};
</script>

<template>
  <div>
    <div id="window">
      <svg width="100%" height="15%">
        <circle
          cx="30"
          cy="30"
          r="10"
          fill="transparent"
          stroke="white"
          stroke-width="2"
          id="close-button"
          @click="closeWindow"
        />
        <circle
          cx="60"
          cy="30"
          r="10"
          fill="transparent"
          stroke="white"
          stroke-width="2"
        />
        <circle
          cx="90"
          cy="30"
          r="10"
          fill="transparent"
          stroke="white"
          stroke-width="2"
        />
      </svg>
      <div id="window-content">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<style scoped>
#window {
  width: 70vw;
  height: 70vh;
  border: 2px solid white;
  border-radius: 10px;
  background-color: rgba(0, 2, 41, 0.8);
  backdrop-filter: blur(10px);
}
#close-button:hover {
  fill: var(--red);
  stroke: var(--red);
}
#window-content {
  margin: 0% 10% 15% 10%;
  height: 70%;
  display: flex;
  align-items: center;
}
</style>
