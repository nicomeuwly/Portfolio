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
        :src="isHovered ? '/img/Folder-Hover.svg' : '/img/Folder.svg'"
        alt="Folder"
        :class="'folder-' + id"
      />
    </div>
    <img
      :src="
        isHovered
          ? '/img/icons/' + icon + '-Icon-Hover.svg'
          : '/img/icons/' + icon + '-Icon.svg'
      "
      :alt="icon + ' icon'"
      class="folder-icon"
    />
    <span class="folder-title" :class="{ hovered: isHovered }">{{
      title
    }}</span>
  </div>
</template>

<style scoped>
.img-container {
  width: 15%;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
}

.folder-content {
  position: relative;
  z-index: 1;
}

.folder-icon {
  position: absolute;
  bottom: 30%;
  z-index: 2;
}

.folder-title {
  margin-top: 10px;
  color: var(--white);
}

.folder-title.hovered {
  font-weight: bold;
}
</style>