<script>
export default {
  name: "Background",
  methods: {
    openLanding(id) {
      this.$emit("open-landing", id);
    },
  },
};
</script>

<template>
  
  <div id="background-items">
    <img src="/img/Logo.svg" alt="Logo Nicolas Meuwly" id="logo" />
    <img src="/img/Corner.svg" alt="Top right corner" class="corner top-right" />
    <img src="/img/Corner.svg" alt="Bottom left corner" class="corner bottom-left" />
    <img src="/img/Avatar.png" alt="Bottom right corner" class="avatar bottom-right" @click="openLanding(0)"/>
  </div>
  <div id="background-gradients">
    <div id="gradient1"></div>
    <div id="gradient2"></div>
    <div id="gradient3"></div>
  </div>
</template>

<style scoped>
#background-items {
  margin: 50px;
  position: absolute;
  z-index: 1;
  width: calc(100% - 100px);
  height: calc(100% - 100px);
}

#logo {
  width: 80px;
  height: 87px;
}

.corner {
  width: 68px;
  height: 68px;
  position: absolute;
}
.avatar {
  width: 100px;
  height: 100px;
  position: absolute;
  border-radius: 50%;
  border: 2px solid var(--white);
  background-color: var(--blue-2);
}
.avatar:hover {
  background-color: transparent;
  transition: background-color 0.5s ease;
}
.top-right {
  top: 0;
  right: 0;
}

.bottom-left {
  bottom: 0;
  left: 0;
  transform: scale(-1, -1);
}
.bottom-right {
  bottom: 0;
  right: 0;
}

#background-gradients {
  position: absolute;
  z-index: 0;
}

#gradient1 {
  background: linear-gradient(90deg, var(--blue) 0%, var(--black) 100%);
  height: calc(100vh / 3);
  width: 100vw;
}

#gradient2 {
  background: linear-gradient(90deg, var(--blue) 0%, var(--black) 100%);
  height: calc(100vh / 3);
  width: calc(100vw * 2 / 3);
}

#gradient3 {
  background: linear-gradient(90deg, var(--blue) 0%, var(--black) 100%);
  height: calc(100vh / 3);
  width: calc(100vw / 3);
}
</style>
