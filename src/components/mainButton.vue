<script>
export default {
  name: "MainButton",
  props: {
    name: String,
    link: String,
  },
};
</script>

<template>
  <div><a :href="link" target="_blank">{{ name }}</a></div>
</template>

<style scoped>
div {
  width: 180px;
  height: 80px;
  background-color: var(--white);
  border-radius: 20px;
  color: var(--blue);
  font-size: 2rem;
  font-weight: bold;
  display: flex;
  justify-content: center;
  align-items: center;
}
div:hover {
  background-color: var(--white-2);
  box-sizing: border-box;
  border: 2px solid var(--white);
  color: var(--white);
}
a {
  color: inherit;
  text-decoration: none;
}
</style>
