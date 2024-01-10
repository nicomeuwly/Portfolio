<script>
import WindowSidePanel from "@/components/WindowSidePanel.vue";
import ColorElement from "@/components/colorElement.vue";
import TypoElement from "@/components/typoElement.vue";
import TechnoElement from "@/components/technoElement.vue";
import MainButton from "@/components/mainButton.vue";
import data from "../data.json";

export default {
  name: "WebsiteWindow",
  components: {
    WindowSidePanel,
    ColorElement,
    TypoElement,
    TechnoElement,
    MainButton,
  },
  data() {
    return {
      activeSection: "Inspirations",
      hoverSection: "",
      titles: data.websiteSectionTitles,
      colors: data.colors,
      typographies: data.typo,
      technologies: data.technologies,
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
      <!-- Section concernant les inspirations -->
      <div
        v-show="activeSection === 'Inspirations'"
        id="inspiration-container"
        class="section-container"
      >
        <h1>Moodboard</h1>
        <div class="content-container">
          <img
            id="moodboard"
            src="/img/Moodboard.png"
            alt="Moodboard"
          />
        </div>
      </div>
      <!-- Section concernant les couleurs -->
      <div
        v-show="activeSection === 'Colors'"
        id="colors-container"
        class="section-container"
      >
        <h1>Palette de couleurs</h1>
        <div class="content-container">
          <ColorElement
            v-for="color in colors"
            :key="color.id"
            :color="color.hex"
            :colorName="color.title"
            :border="color.border"
            class="color-element"
          />
          <p class="comment">
            Des variantes de ces couleurs avec différents niveaux d’opacité ont
            également été utilisées.
          </p>
        </div>
      </div>
      <!-- Section concernant la typographie -->
      <div
        v-show="activeSection === 'Typography'"
        id="typography-container"
        class="section-container"
      >
        <h1>Typographie</h1>
        <div class="content-container">
          <TypoElement
            v-for="typo in typographies"
            :key="typo.id"
            :title="typo.title"
            :usage="typo.usage"
            :fontWeight="typo.fontWeight"
          />
        </div>
      </div>
      <!-- Section concernant les technologies -->
      <div
        v-show="activeSection === 'Technology'"
        id="technology-container"
        class="section-container"
      >
        <h1>Technologies</h1>
        <div class="content-container">
          <TechnoElement
            v-for="techno in technologies"
            :key="techno.id"
            :title="techno.title"
            :description="techno.description"
            :image="techno.icon"
          />
          <MainButton
            :name="'GitHub repository'"
            :link="'https://github.com/nicomeuwly/Portfolio'"
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
  padding: 5%;
  display: flex;
  justify-content: center;
  gap: 30px;
}
#colors-container .content-container {
  flex-direction: row;
  flex-wrap: wrap;
}
#typography-container .content-container {
  flex-direction: colomn;
  flex-wrap: wrap;
}
#technology-container .content-container {
  flex-wrap: wrap;
}
h1 {
  color: var(--white);
}

#moodboard {
  width: 90%;
}

#colors-container .content-container {
  margin-left: 10%;
  margin-right: 10%;
}
.comment {
  color: var(--white);
  text-align: center;
  font-size: 1rem;
  margin: 0;
  width: 100%;
}
</style>
