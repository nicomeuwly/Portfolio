<script>
import WindowSidePanelEqual from "@/components/WindowSidePanelEqual.vue";
import MainButton from "@/components/mainButton.vue";
import data from "../data.json";

export default {
  name: "JobWindow",
  components: {
    WindowSidePanelEqual,
    MainButton,
  },
  props: {
    jobId: Number,
  },
  data() {
    return {
      job: data.jobs[this.jobId],
    };
  },
  methods: {
    receiveDataFromChild(data) {
      this.$emit("parent-to-grandparent", data);
    },
  },
};
</script>

<template>
  <WindowSidePanelEqual @child-to-parent="receiveDataFromChild">
    <template v-slot:left-side-panel>
      <div class="left-side">
        <h1>{{ job.title }}</h1>
        <p>{{ job.description }}</p>
        <div class="tags-container">
          <span v-for="tag in job.tags" :key="tag" class="tag">{{ tag }}</span>
        </div>
      </div>
    </template>
    <template v-slot:right-side-panel>
      <div class="right-side">
        <img :src="'/Portfolio/img/jobs/' + job.image" alt="job image" />
        <MainButton
          v-for="link in job.links"
          :key="link.title"
          :name="link.title"
          :link="link.url"
        />
      </div>
    </template>
  </WindowSidePanelEqual>
</template>

<style scoped>
.left-side {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
  width: 100%;
}
.right-side {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
  width: 100%;
}
h1,
p {
  color: var(--white);
  margin: 0;
}
.tags-container {
  display: flex;
  gap: 10px;
}
.tag {
  background-color: var(--white-2);
  color: var(--white);
  border-radius: 10px;
  padding: 10px;
}
img {
  max-width: 100%;
  max-height: 60%;
}
MainButton {
  width: 50%;
}
</style>
