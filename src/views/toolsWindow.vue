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
      activeSection: "Devlopment",
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
          <img
            :src="
              isActiveSection(title.icon) || isHoveredSection(title.icon)
                ? '/Portfolio/img/icons/' + title.icon + '-Icon-Active.svg'
                : '/Portfolio/img/icons/' + title.icon + '-Icon.svg'
            "
            :alt="title.icon + ' Icon'"
          />
          {{ title.title }}
        </li>
      </ul>
    </template>
    <template v-slot:right-side-panel>
      <!-- Section concernant les compétences en développement -->
      <div
        v-show="activeSection === 'Devlopment'"
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
        v-show="activeSection === 'Creation'"
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
  gap: 25px;
}

li {
  color: var(--white-2);
  font-size: 1.5rem;
  display: flex;
  align-items: center;
  list-style: none;
}

li:hover {
  color: var(--white);
  cursor: pointer;
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
}

.content-container {
  max-width: 760px;
  
  margin: 5%;
  display: flex;
  justify-content: center;
  
  flex-direction: row;
  flex-wrap: wrap;
  gap: 40px 70px;
}
#development-container .content-container {
  max-height: 440px;
  overflow-x: hidden;
  overflow-y: auto;
}

#creation-container .content-container{
  height: 100%;
}

.content-container::-webkit-scrollbar {
  display: none;
}

h1 {
  color: var(--white);
}

</style>
