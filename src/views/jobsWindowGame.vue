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
      characterPosition: { x: 50, y: 300 },
      blocks: [{ id: 1, position: { x: 150, y: 160 } }, { id: 2, position: { x: 300, y: 160 } }, { id: 3, position: { x: 450, y: 160 } }],
    };
  },
  methods: {
    receiveDataFromChild(data) {
      this.$emit("parent-to-grandparent", data);
    },
  },
  mounted() {
    console.log(this.activeWindow);
  },
};
</script>

<template>
  <Window @child-to-parent="receiveDataFromChild">
    <Character :position="characterPosition" />
    <Block v-for="block in blocks" :key="block.id" :position="block.position" />
  </Window>
</template>

<style scoped></style>