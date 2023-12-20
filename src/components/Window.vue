<script>
export default {
    name: "Window",
    data() {
        return {
            window: document.getElementById("window"),
            closeButton: document.getElementById("close-button"),
            windowContent: document.getElementById("window-content"),
        };
    },
    methods: {
        closeWindow() {
            const window = document.getElementById("window");
            window.style.display = "none";
        },
    },
};
</script>

<template>
    <div id="window">
        <svg>
            <circle cx="30" cy="30" r="10" fill="transparent" stroke="white" stroke-width="2" id="close-button"
                @click="closeWindow()" />
            <circle cx="60" cy="30" r="10" fill="transparent" stroke="white" stroke-width="2" />
            <circle cx="90" cy="30" r="10" fill="transparent" stroke="white" stroke-width="2" />
        </svg>
        <div id="window-content">

        </div>
    </div>
</template>

<style scoped>
#window {
    display: none;
    position: absolute;
    width: 80vw;
    height: 70vh;
    border: 2px solid white;
    border-radius: 10px;
    background-color: rgba(0, 2, 41, 0.8);
    backdrop-filter: blur(10px);
    z-index: 3;
}

#close-button:hover {
    fill: var(--red);
    stroke: var(--red);
}
</style>