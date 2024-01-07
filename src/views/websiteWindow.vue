<script>
import WindowSidePanel from "@/components/WindowSidePanel.vue";
import data from "../data.json";

export default {
  name: "WebsiteWindow",
  components: {
    WindowSidePanel
  },
  data() {
    return {
      activeSection: 'Inspirations',
      titles: data.websiteSectionTitles,
    }
  },
  methods: {
    receiveDataFromChild(data) {
      this.$emit("parent-to-grandparent", data);
    },
    setActiveSection(section) {
      this.activeSection = section;
    },
    isActiveSection(section) {
      return this.activeSection === section;
    },
  },
};
</script>

<template>
  <WindowSidePanel @child-to-parent="receiveDataFromChild">
    <template v-slot:left-side-panel>
      <ul>
        <li v-for="title in titles" :key="title" @click="setActiveSection(title.icon)"
          :class="{ active: isActiveSection(title.icon) }">
          <img :src="!isActiveSection(title.icon) ? '/Portfolio/img/icons/' + title.icon + '-Icon.svg' : '/Portfolio/img/icons/' + title.icon + '-Icon-Active.svg'" :alt="title.icon + ' Icon'" />
          {{ title.title }}
        </li>
      </ul>
    </template>
    <template v-slot:right-side-panel>
      <div v-show="activeSection === 'Inspirations'" id="inspiration-container" class="section-container">
        <h1>Moodboard</h1>
        <div class="content-container">

        </div>
      </div>
      <div v-show="activeSection === 'Colors'" id="colors-container" class="section-container">
        <h1>Palette de couleurs</h1>
        <div class="content-container">

        </div>
      </div>
      <div v-show="activeSection === 'Typography'" id="typography-container" class="section-container">
        <h1>Typographie</h1>
        <div class="content-container">

        </div>
      </div>
      <div v-show="activeSection === 'Technology'" id="technology-container" class="section-container">
        <h1>Technologies</h1>
        <div class="content-container">

        </div>
      </div>
    </template>
  </WindowSidePanel>
</template>

<style scoped>
ul {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: left;
  gap: 25px;
}

li {
  color: var(--white-2);
  font-size: 1.5rem;
  display: flex;
  align-items: center;
  list-style: none;
}

li img {
  width: 40px;
  height: 40px;
  margin-right: 20px;
}

li.active {
  color: var(--white);
}

.section-container {
  width: 100%;
  height: 100%;
  margin-top: 5%;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 25px;
}

h1 {
  color: var(--white);
}</style>
