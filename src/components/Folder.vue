<script>
export default {
  name: "Folder",
  props: {
    id: Number,
    title: String,
    icon: String,
  },
  data() {
    return {
      isHovered: false,
    };
  },
  methods: {
    changeImageSource(isHovered) {
      this.isHovered = isHovered;
    },
  },
};
</script>

<template>
  <div
    class="img-container"
    @mouseover="changeImageSource(true)"
    @mouseout="changeImageSource(false)"
  >
    <div class="folder-content">
      <img
        :src="isHovered ? '/img/folders/Folder-'+ icon +'-Hover.svg' : '/img/folders/Folder-'+ icon +'.svg'"
        alt="Content folder"
        class="folder"
      />
    </div>
    <span class="folder-title" :class="{ hovered: isHovered }">{{
      title
    }}</span>
  </div>
</template>

<style scoped>
.img-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  width: 12%;
}

.folder-content {
  position: relative;
  z-index: 1;
}

.folder {
  width: 100%;
}

.folder-title {
  margin-top: 5%;
  color: var(--white-2);
}

.folder-title.hovered {
  color: var(--white);
}
</style>