<script>
export default {
    name: "TypoElement",
    props: {
        title: String,
        usage: String,
        fontWeight: String,
    },
    methods: {
        applyStyle(style) {
            switch (style) {
                case 'bold':
                    return 'bold-text';
                case 'normal':
                    return 'normal-text';
            }
        },
    },
};
</script>

<template>
    <div class="typo-container">
        <h2 :class="applyStyle(fontWeight)">{{ title }}</h2>
        <p :class="applyStyle(fontWeight)">ABCDEFGHIJKLMNOPQRSTUVWXYZ<br>abcdefghijklmnopqrstuvwxyz</p>
        <div class="line"></div>
        <p :class="applyStyle(fontWeight)">1234567890</p>
        <div class="line"></div>
        <p :class="applyStyle(fontWeight)">{{ usage }}</p>
    </div>
</template>

<style scoped>
.typo-container {
    background-color: var(--white);
    border-radius: 15px;
    width: 300px;
    height: 200px;
    padding: 10px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}
h2 {
    font-weight: normal;
    font-size: 1rem;
}
p {
    font-size: 0.8rem;
}
.line {
    width: 100%;
    height: 1px;
    background-color: var(--black);
}
.bold-text{
    font-weight: bold;
}
.regular-text {
    font-weight: normal;
}
</style>