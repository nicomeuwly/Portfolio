<script>
export default {
  name: "ColorElement",
  props: {
    color: String,
    colorName: String,
    border: Boolean,
  },
};
</script>

<template>
    <div class="color-container">
        <div :style="{ backgroundColor: color }" :class="{ border: border }"></div>
        <p>{{ color }}</p>
        <h2>{{ colorName }}</h2>
    </div>
</template>

<style scoped>
.color-container {
    width: 100px;
    height: 150px;
    padding: 8px;
    background-color: var(--white);
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    align-items: left;
    justify-content: flex-start;
    gap: 6px;
}
.color-container div {
    width: 100%;
    padding-top: 100%;
}
.border {
    border: 1px solid var(--black);
}

h2 {
    margin: 0;
    font-size: 1rem;
}
p {
    margin: 0;
    font-size: 0.8rem;
}
</style>