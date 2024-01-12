<script>
import Folder from "@/components/Folder.vue";
import LandingWindow from "./landingWindow.vue";
import AboutWindow from "./aboutWindow.vue";
import PathWindow from "./pathWindow.vue";
import JobsWindow from "./jobsWindow.vue";
import JobsWindowGame from "./jobsWindowGame.vue";
import ToolsWindow from "./toolsWindow.vue";
import WebsiteWindow from "./websiteWindow.vue";
import Background from "@/components/background.vue";

export default {
  name: "Home",
  components: {
    Folder,
    LandingWindow,
    AboutWindow,
    PathWindow,
    JobsWindow,
    JobsWindowGame,
    ToolsWindow,
    WebsiteWindow,
    Background
},
  data() {
    return {
      folders: {
        1: {
          title: "A PROPOS",
          icon: "Info",
        },
        2: {
          title: "PARCOURS",
          icon: "Path",
        },
        3: {
          title: "REALISATIONS",
          icon: "Jobs",
        },
        4: {
          title: "OUTILS",
          icon: "Tools",
        },
        5: {
          title: "CE SITE",
          icon: "Website",
        },
      },
      isWindowOpen: false,
      activeWindowId: null,
    };
  },
  methods: {
    receiveDataFromParent(data) {
      this.isWindowOpen = data;
    },
    openWindow(id) {
      this.isWindowOpen = true;
      this.activeWindowId = id;
    },
    handleOpenWindow(id) {
      this.openWindow(id);
    },
    openLandingWindowAfterLoading() {
      setTimeout(() => {
        this.openWindow(0);
      }, 1000);
    },
  },
  mounted() {
    this.openLandingWindowAfterLoading();
  },
};
</script>

<template>
  <div id="content">
    <Folder
      v-for="(folder, id) in folders"
      :key="parseInt(id)"
      :id="parseInt(id)"
      :title="folder.title"
      :icon="folder.icon"
      @click="openWindow(parseInt(id))"
    />
    <LandingWindow
      class="window"
      v-if="isWindowOpen && activeWindowId === 0"
      @parent-to-grandparent="receiveDataFromParent"
    />
    <AboutWindow
      class="window"
      v-if="isWindowOpen && activeWindowId === 1"
      @parent-to-grandparent="receiveDataFromParent"
    />
    <PathWindow
      class="window"
      v-if="isWindowOpen && activeWindowId === 2"
      @parent-to-grandparent="receiveDataFromParent"
    />
    <JobsWindow
      class="window"
      v-if="isWindowOpen && activeWindowId === 3"
      @parent-to-grandparent="receiveDataFromParent"
      @open-game="handleOpenWindow"
      :activeWindow="activeWindowId"
    />
    <JobsWindowGame
      class="window"
      v-if="isWindowOpen && activeWindowId === 12"
      @parent-to-grandparent="receiveDataFromParent"
      :activeWindow="activeWindowId"
    />
    <ToolsWindow
      class="window"
      v-if="isWindowOpen && activeWindowId === 4"
      @parent-to-grandparent="receiveDataFromParent"
    />
    <WebsiteWindow
      class="window"
      v-if="isWindowOpen && activeWindowId === 5"
      @parent-to-grandparent="receiveDataFromParent"
    />
  </div>
  <Background @open-landing="handleOpenWindow"/>
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
.window {
  position: absolute;
  z-index: 3;
}
</style>
