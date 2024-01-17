<script>
export default {
  name: "Block",
};
</script>

<template>
  <div class="block">
    <span class="material-symbols-rounded">question_mark</span>
  </div>
</template>

<style scoped>
.block {
  width: 120px;
  height: 120px;
  background-color: var(--white);
  border-radius: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  transition: transform 0.5s ease-in-out
}
.block:hover {
  transform: translateY(-15px);
}
span {
  font-size: 4rem;
  color: var(--blue);
  margin: 0;
}
img {
  width: 20px;
  height: 20px;
  position: relative;
  z-index: 0;
}
</style>
