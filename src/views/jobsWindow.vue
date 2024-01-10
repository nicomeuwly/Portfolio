<script>
import Window from "@/components/Window.vue";

export default {
  name: "JobsWindow",
  components: {
    Window,
  },
  props: {
    activeWindow: Number,
  },
  methods: {
    receiveDataFromChild(data) {
      this.$emit("parent-to-grandparent", data);
    },
    openGame(id) {
      this.$emit("open-game", id);
    },
    handleKeyPress(key) {
      switch (key) {
        case "ArrowLeft":
        case "a":
          this.$refs.moveLeft.style.backgroundColor = "var(--white-2)";
          break;
        case "ArrowRight":
        case "d":
          this.$refs.moveRight.style.backgroundColor = "var(--white-2)";
          break;
        case " ":
          this.$refs.jump.style.backgroundColor = "var(--white-2)";
          break;
      }
    },
    handleKeyUp(key) {
      switch (key) {
        case "ArrowLeft":
        case "a":
          this.$refs.moveLeft.style.backgroundColor = "";
          break;
        case "ArrowRight":
        case "d":
          this.$refs.moveRight.style.backgroundColor = "";
          break;
        case " ":
          this.$refs.jump.style.backgroundColor = "";
          break;
      }
    },
  },
  mounted() {
    if (this.activeWindow === 3) {
      window.addEventListener("keydown", (e) => {
        this.handleKeyPress(e.key);
      });
      window.addEventListener("keyup", (e) => {
        this.handleKeyUp(e.key);
      });
    }
    console.log(this.activeWindow);
  },
};
</script>

<template>
  <Window @child-to-parent="receiveDataFromChild">
    <div class="controls">
      <div class="control-container move">
        <h2>Se déplacer</h2>
        <div>
          <span ref="moveLeft" class="material-symbols-rounded control"
            >arrow_back</span
          >
          <span ref="moveRight" class="material-symbols-rounded control"
            >arrow_forward</span
          >
        </div>
      </div>
      <div class="control-container jump">
        <h2>Sauter</h2>
        <span ref="jump" class="material-symbols-rounded control"
          >space_bar</span
        >
      </div>
      <div class="control-container">
        <h2>Démarrer</h2>
        <span class="material-symbols-rounded start" @click="openGame(12)"
          >play_arrow</span
        >
      </div>
    </div>
  </Window>
</template>

<style scoped>
.controls {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 100%;
  height: 100%;
}
.control {
  border: 2px solid var(--white);
  font-size: 4rem;
  padding: 0.5rem;
  color: var(--white);
  border-radius: 20px;
  text-align: center;
  cursor: pointer;
  transition: background-color 0.2s ease-in-out;
}
h2 {
  color: var(--white);
  font-size: 2rem;
}
.control-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 200px;
}
.control-container div {
  display: flex;
  justify-content: space-between;
  width: 100%;
}
.jump span {
  width: 180.8px;
}
.start {
  font-size: 5rem;
  fill: 1;
  background-color: var(--white);
  border: 2px solid var(--white);
  color: var(--blue);
  border-radius: 100%;
  text-align: center;
  cursor: pointer;
  transition: background-color 0.2s ease-in-out, color 0.2s ease-in-out;
}
.start:hover {
  background-color: var(--white-2);
  color: var(--white);
}

.material-symbols-rounded {
  font-variation-settings: "FILL" 1, "wght" 400, "GRAD" 0, "opsz" 24;
}
</style>
