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
  min-width: 100px;
  height: 60px;
  padding-left: 20px;
  padding-right: 20px;
  background-color: var(--white);
  border: 2px solid transparent;
  border-radius: 20px;
  color: var(--blue);
  font-size: 1.5rem;
  font-weight: bold;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: background-color 0.2s ease-in-out, color 0.2s ease-in-out, border 0.2s ease-in-out;
}
div:hover {
  background-color: var(--white-2);
  border: 2px solid var(--white);
  color: var(--white);
}
a {
  color: inherit;
  text-decoration: none;
}
</style>
