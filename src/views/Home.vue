<script>
import Folder from "@/components/Folder.vue";
import Window from "@/components/Window.vue";

export default {
  name: "Home",
  components: {
    Folder,
    Window,
  },
  methods: {
    openWindow() {
      const window = document.getElementById("window");
      window.style.display = "block";
    },
  },
};

const viewportHeight = window.innerHeight;
const viewportWidth = window.innerWidth;

const setGradients = () => {
  const gradient1 = document.getElementById("gradient1");
  gradient1.style.height = `${viewportHeight / 3}px`;
  gradient1.style.width = `${viewportWidth}px`;

  const gradient2 = document.getElementById("gradient2");
  gradient2.style.height = `${viewportHeight / 3}px`;
  gradient2.style.width = `${(viewportWidth * 2) / 3}px`;

  const gradient3 = document.getElementById("gradient3");
  gradient3.style.height = `${viewportHeight / 3}px`;
  gradient3.style.width = `${viewportWidth / 3}px`;
};

window.onload = () => {
  setGradients();
};

window.addEventListener("resize", () => {
  setGradients();
});
</script>

<template>
  <div id="content">
    <Folder :id="1" icon="Info" title="A PROPOS" @click="openWindow()"/>
    <Folder :id="2" icon="Path" title="PARCOURS" @click="openWindow()"/>
    <Folder :id="3" icon="Jobs" title="REALISATIONS" @click="openWindow()"/>
    <Folder :id="4" icon="Tools" title="OUTILS" @click="openWindow()"/>
    <Folder :id="5" icon="Website" title="CE SITE" @click="openWindow()"/>
    <Window />
  </div>
  <div id="background-items">
    <img src="/img/Logo.svg" alt="Logo Nicolas Meuwly" id="logo" />
    <img
      src="/img/Corner.svg"
      alt="Top right corner"
      class="corner top-right"
    />
    <img
      src="/img/Corner.svg"
      alt="Bottom left corner"
      class="corner bottom-left"
    />
  </div>
  <div id="background-gradients">
    <div id="gradient1"></div>
    <div id="gradient2"></div>
    <div id="gradient3"></div>
  </div>
</template>

<style>
#content {
  margin: 150px;
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2;
  width: calc(100% - 300px);
  height: calc(100% - 300px);
}
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
.top-right {
  top: 0;
  right: 0;
}
.bottom-left {
  bottom: 0;
  left: 0;
  transform: scale(-1, -1);
}
#gradient1 {
  background: linear-gradient(90deg, var(--blue) 0%, var(--black) 100%);
}
#gradient2 {
  background: linear-gradient(90deg, var(--blue) 0%, var(--black) 100%);
}
#gradient3 {
  background: linear-gradient(90deg, var(--blue) 0%, var(--black) 100%);
}
</style>
