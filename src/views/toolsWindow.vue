<script>
import WindowSidePanel from "@/components/WindowSidePanel.vue";
import SkillElement from "@/components/skillElement.vue";
import data from "../data.json";

export default {
  name: "ToolsWindow",
  components: {
    WindowSidePanel,
    SkillElement,
  },
  data() {
    return {
      activeSection: "code",
      hoverSection: "",
      titles: data.skillsSectionTitles,
      devSkills: data.devSkills,
      creationSkills: data.creationSkills,
    };
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
    isHoveredSection(section) {
      return this.hoverSection === section;
    },
  },
};
</script>

<template>
  <WindowSidePanel @child-to-parent="receiveDataFromChild">
    <template v-slot:left-side-panel>
      <ul>
        <li
          v-for="title in titles"
          :key="title"
          @click="setActiveSection(title.icon)"
          :class="{ active: isActiveSection(title.icon) }"
          @mouseover="hoverSection = title.icon"
          @mouseout="hoverSection = ''"
        >
          <span class="material-symbols-rounded">{{ title.icon }}</span>
          {{ title.title }}
        </li>
      </ul>
    </template>
    <template v-slot:right-side-panel>
      <!-- Section concernant les compétences en développement -->
      <div
        v-show="activeSection === 'code'"
        id="development-container"
        class="section-container"
      >
        <h1>Développement</h1>
        <div class="content-container">
          <SkillElement
            v-for="skill in devSkills"
            :key="skill.title"
            :title="skill.title"
            :icon="skill.icon"
            :level="skill.level"
          />
        </div>
      </div>
      <!-- Section concernant les compétences en création -->
      <div
        v-show="activeSection === 'brush'"
        id="creation-container"
        class="section-container"
      >
        <h1>Création</h1>
        <div class="content-container">
          <SkillElement
            v-for="skill in creationSkills"
            :key="skill.title"
            :title="skill.title"
            :icon="skill.icon"
            :level="skill.level"
          />
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
  gap: 2rem;
}

li {
  color: var(--white-2);
  font-size: 1.5rem;
  display: flex;
  align-items: center;
  list-style: none;
  gap: 1rem;
}

.material-symbols-rounded {
  font-variation-settings: "FILL" 0, "wght" 400, "GRAD" 0, "opsz" 24;
  font-size: 3rem;
}

li:hover {
  color: var(--white);
  cursor: pointer;
}

li.active {
  color: var(--white);
}

.section-container {
  width: 100%;
  height: 90%;
  background-color: var(--blue-dark);
  margin-top: 5%;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5%;
}

.content-container {
  width: 90%;
  max-height: 450px;
  min-height: 188px;
  display: flex;
  justify-content: center;
  flex-direction: row;
  flex-wrap: wrap;
  overflow-x: hidden;
  overflow-y: auto;
  gap: 40px 70px;
}

.content-container::-webkit-scrollbar {
  display: none;
}

h1 {
  color: var(--white);
}

</style>
