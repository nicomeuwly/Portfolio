<script>
import Window from "@/components/Window.vue";
import Character from "@/components/character.vue";
import Block from "@/components/block.vue";

export default {
  name: "JobsWindowGame",
  components: {
    Window,
    Character,
    Block,
  },
  props: {
    activeWindow: Number,
  },
  data() {
    return {
      blocks: [1, 2, 3, 4, 5],
      characterPosition: {
        x: 0,
        y: 80,
      },
    };
  },
  methods: {
    receiveDataFromChild(data) {
      this.$emit("parent-to-grandparent", data);
    },
  },
};
</script>

<template>
  <Window @child-to-parent="receiveDataFromChild">
    <div class="game-container" ref="container">
      <div class="block-container">
        <Block v-for="block in blocks" :key="block.id" :position="block.position" />
      </div>
      <Character
        :position="characterPosition"
        :maxLeftPosition="0"
        :maxRightPosition="1000"
      />
      <div class="floor"></div>
    </div>
  </Window>
</template>

<style scoped>
.game-container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-wrap: wrap;
  align-content: space-between;
}
.block-container {
  width: 100%;
  display: flex;
  justify-content: space-around;
  position: relative;
  top: 20px;
}
.floor {
  width: 100%;
  height: 20px;
  background-color: var(--white);
  border-radius: 20px;
}
</style>
