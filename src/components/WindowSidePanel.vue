<script>
export default {
    name: "WindowSidePanel",
    methods: {
        closeWindow() {
            this.$emit("child-to-parent", false);
        },
    },
};
</script>

<template>
    <div>
        <div id="window">
            <svg width="100%" height="15%">
                <circle cx="30" cy="30" r="10" fill="transparent" stroke="white" stroke-width="2" id="close-button"
                    @click="closeWindow" />
                <circle cx="60" cy="30" r="10" fill="transparent" stroke="white" stroke-width="2" />
                <circle cx="90" cy="30" r="10" fill="transparent" stroke="white" stroke-width="2" />
            </svg>
            <div id="left-side-panel">
                <div id="left-side-panel-content">
                    <slot name="left-side-panel"></slot>
                </div>
            </div>
            <div id="right-side-panel">
                <div id="right-side-panel-content">
                    <slot name="right-side-panel"></slot>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
#window {
    width: 70vw;
    height: 70vh;
    border: 2px solid var(--white);
    border-radius: 10px;
    background-color: var(--blue-dark-2);
    backdrop-filter: blur(10px);
}

#close-button:hover {
    fill: var(--red);
    stroke: var(--red);
    transition: fill 0.3s ease, stroke 0.3s ease;
}

#right-side-panel {
    width: 70%;
    height: 100%;
    background-color: var(--blue-dark);
    border-radius: 0 10px 10px 0;
    border-left: 2px solid var(--white);
    position: absolute;
    top: 0;
    right: 0;
}
#left-side-panel {
    padding-top: 5%;
}
</style>
