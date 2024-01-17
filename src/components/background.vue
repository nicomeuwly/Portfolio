<script>
export default {
  name: "Background",
  emits: ["open-landing"],
  methods: {
    openLanding(id) {
      this.$emit("open-landing", id);
    },
    setItemsPosition() {
      const logo = this.$refs.logo;
      const avatar = this.$refs.avatar;
      const cornerTopRight = this.$refs.cornerTopRight;
      const cornerBottomLeft = this.$refs.cornerBottomLeft;
      const space = window.innerWidth * 0.03;
      logo.style.top = `${space}px`;
      logo.style.left = `${space}px`;
      avatar.style.bottom = `${space}px`;
      avatar.style.right = `${space}px`;
      cornerTopRight.style.top = `${space}px`;
      cornerTopRight.style.right = `${space}px`;
      cornerBottomLeft.style.bottom = `${space}px`;
      cornerBottomLeft.style.left = `${space}px`;
    },
    returnToHome() {
      window.location.href = "/";
    },
  },
  mounted() {
    this.setItemsPosition();
    window.addEventListener("resize", this.setItemsPosition);
  },
};
</script>

<template>
  <div id="background">
    <div id="background-items">
      <img src="/img/Logo.svg" alt="Logo Nicolas Meuwly" id="logo" ref="logo" @click="returnToHome"/>
      <img
        src="/img/Corner.svg"
        alt="Top right corner"
        class="corner top-right"
        ref="cornerTopRight"
      />
      <img
        src="/img/Corner.svg"
        alt="Bottom left corner"
        class="corner bottom-left"
        ref="cornerBottomLeft"
      />
      <img
        src="/img/Avatar.png"
        alt="Bottom right corner"
        class="avatar bottom-right"
        ref="avatar"
        @click="openLanding(0)"
      />
    </div>
    <div id="background-gradients">
      <div id="gradient1"></div>
      <div id="gradient2"></div>
      <div id="gradient3"></div>
    </div>
  </div>
</template>

<style scoped>

#background {
  width: 100%;
  height: 100%;
}
#background-items {
  position: absolute;
  z-index: 1;
  width: 100%;
  height: 100%;
}

#logo {
  width: 5%;
  aspect-ratio: 1/1;
  position: absolute;
}

.corner {
  width: 5%;
  aspect-ratio: 1/1;
  position: absolute;
}
.avatar {
  width: 5%;
  aspect-ratio: 1/1;
  position: absolute;
  border-radius: 50%;
  border: 2px solid var(--white);
  background-color: var(--blue-2);
}
.avatar:hover {
  background-color: transparent;
  transition: background-color 0.5s ease;
}

.bottom-left {
  transform: scale(-1, -1);
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
