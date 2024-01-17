<script>
import Window from "@/components/Window.vue";
import ListElement from "@/components/listElement.vue";
import data from "../data.json";

export default {
  name: "PathWindow",
  components: {
    Window,
    ListElement,
  },
  methods: {
    receiveDataFromChild(data) {
      this.$emit("parent-to-grandparent", data);
    },
    setLinePosition() {
      const circleLeftPosition = document.querySelector("svg").getBoundingClientRect().left;
      const circleWidth = this.$refs.container.offsetWidth * 0.08;
      const windowMargin = window.innerWidth*0.7*0.05;
      const containerGap = this.$refs.container.offsetWidth * 0.03;
      const lineWidth = circleLeftPosition - windowMargin + circleWidth/2 + containerGap;
      this.$refs.line.style.left = `${lineWidth}px`;
    },
    switchList() {
      this.toggleOn = !this.toggleOn;
    },
  },
  data() {
    return {
      education: data.education,
      experience: data.experience,
      toggleOn: false,
    }
  },
  mounted() {
    this.setLinePosition();
    window.addEventListener("resize", this.setLinePosition);
  },
  computed: {
    reversedEducation() {
      return Object.keys(this.education).reverse().map(key => this.education[key]);
    },
    reversedExperience() {
      return Object.keys(this.experience).reverse().map(key => this.experience[key]);
    },
  }
};
</script>

<template>
  <Window @child-to-parent="receiveDataFromChild">
    <div class="toggle-button-container">
      <p :class="{ 'active-text': !toggleOn }" class="formation">Formation</p>
      <label class="switch">
        <input type="checkbox" @change="switchList" />
        <span></span>
      </label>
      <p :class="{ 'active-text': toggleOn }" class="experience">Expérience</p>
    </div>
    <div class="list-element-container" ref="container">
      <ListElement v-if="!toggleOn" v-for="(element, id) in reversedEducation" :key="parseInt(id)" :id="parseInt(id)"
        :idName="'education'" :title="element.title" :date="element.date" :description="element.description" />
      <ListElement v-if="toggleOn" v-for="(element, id) in reversedExperience" :key="parseInt(id)" :id="parseInt(id)"
        :idName="'experience'" :title="element.title" :date="element.date" :description="element.description" />
    </div>
    <div class="bg-line" ref="line"></div>
  </Window>
</template>

<style scoped>
.list-element-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 20%;
  height: 100%;
  width: 100%;
  overflow-y: scroll;
  z-index: 1;
}

.list-element-container::-webkit-scrollbar {
  display: none;
}

.bg-line {
  width: 2px;
  height: 75%;
  background-color: var(--white);
  z-index: 0;
  position: absolute;
}

.toggle-button-container {
  position: absolute;
  top: 3%;
  right: 4%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10%;
  width: 22%;
}

.switch {
  display: inline-block;
  position: relative;
  width: 70px;
  height: 40px;
  cursor: pointer;
  overflow: hidden;
  caret-color: transparent;
}

.switch input {
  position: absolute;
  top: -30px;
  left: -30px;
  width: 0;
  height: 0;
}

.switch input+span {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(255, 255, 255, 0.6);
  border-radius: 22.5px;
}

.switch input:checked+span {
  background: rgba(255, 255, 255, 0.6);
}

.switch input+span:before {
  content: "";
  display: inline-block;
  position: absolute;
  top: 50%;
  left: 4px;
  width: 32px;
  height: 32px;
  background: var(--white);
  border-radius: 50%;
  transform: translateY(-50%);
  transition: all .5s;
}

.switch input:checked+span:before {
  left: 34px;
}

p {
  color: var(--white-2);
  width: 30%;
}

.formation {
  text-align: right;
}

.experience {
  text-align: left;
}

.active-text {
  color: var(--white);
}
</style>
