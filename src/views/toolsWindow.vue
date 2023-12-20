<script>
import Window from "@/components/Window.vue";

export default {
  name: "ToolsWindow",
  components: {
    Window,
  },
  methods: {
    receiveDataFromChild(data) {
      this.$emit("parent-to-grandparent", data);
    },
  },
};
</script>

<template>
  <Window @child-to-parent="receiveDataFromChild"></Window>
</template>

<style scoped></style>
