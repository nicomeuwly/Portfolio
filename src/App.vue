<script>
import Home from "@/views/Home.vue";

export default {
  name: "App",
  components: {
    Home,
  },
};
</script>

<template>
  <div id="portfolio">
    <Home />
  </div>
</template>

<style>
#portfolio {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
}
</style>
