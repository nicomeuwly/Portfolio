<script>
export default {
    name: "TechnoElement",
    props: {
        title: String,
        description: String,
        image: String,
    },
};
</script>

<template>
    <div class="techno-container">
        <div class="text-container">
            <h2>{{ title }}</h2>
            <p>{{ description }}</p>
        </div>
        <div class="img-container">
            <img :src="'/img/logos/' + image + '.png'" :alt="image + ' logo'">
        </div>
    </div>
</template>

<style scoped>
.techno-container {
    display: flex;
    flex-direction: colomn;
    justify-content: space-between;
    align-items: center;
    background-color: var(--white);
    border-radius: 10px;
    padding: 20px;
    width: 70%;
    height: 15%;
}
img {
    width: 70px;
    height: 70px;
}
h2, p {
    margin: 5px;
}
</style>