<script>
import Folder from "@/components/Folder.vue";

export default {
  name: "Home",
  components: {
    Folder,
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
    <Folder class="folder"/>
    <Folder class="folder"/>
    <Folder class="folder"/>
    <Folder class="folder"/>
    <Folder class="folder"/>
  </div>
  <div id="background-items">
    <img src="/img/Logo.png" alt="Logo Nicolas Meuwly" id="logo" />
    <img
      src="/img/Corner.png"
      alt="Top right corner"
      class="corner top-right"
    />
    <img
      src="/img/Corner.png"
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
  gap: 90px;
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
