<script>
import Window from "@/components/Window.vue";

export default {
    name: "LandingWindow",
    components: {
        Window,
    },
    methods: {
        receiveDataFromChild(data) {
            this.$emit("parent-to-grandparent", data);
        },
        setBubbleTextMargins() {
            const bubbleContent = document.querySelector("#bubble-content");
            const bubbleText = document.querySelector(".bubble-text");
            const bubbleTextHeight = bubbleText.offsetHeight;
            const allBubbbleTexts = bubbleContent.querySelectorAll(".bubble-text");
            allBubbbleTexts.forEach((bubbleText) => {
                bubbleText.style.padding = `${(90 - parseInt(bubbleTextHeight)) / 2}px`;
            });
        },
    },
    mounted() {
        this.setBubbleTextMargins();
    },
};
</script>

<template>
    <Window @child-to-parent="receiveDataFromChild">
        <div id="landing-window-content">
            <div id="left-side">
                <p>Nicolas Meuwly</p>
                <div id="bubble-container">
                    <img src="/img/Bubble.svg" />
                    <div id="bubble-content">
                        <p class="bubble-text">Développeur web</p>
                        <p class="bubble-text">Designer UI</p>
                        <p class="bubble-text">Gamer...</p>
                    </div>
                </div>
            </div>
            <img src="/img/Avatar.png" id="avatar" />
        </div>
    </Window>
</template>

<style scoped>
#landing-window-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    height: 100%;
}

#avatar {
    height: 70%;
    border-radius: 50%;
    border: 2px solid var(--white);
    background-color: var(--blue-2);
}


#left-side>p {
    color: var(--white);
    font-size: 2rem;
    margin-bottom: 0.5em;
}

#bubble-container>img {
    position: absolute;
    z-index: -1;
}

#bubble-container {
    overflow: hidden;
    height: 90px;
}

.bubble-text {
    color: var(--blue);
    font-size: 2rem;
    font-weight: bold;
    position: relative;
    margin: 0;
    animation: text-animation 5s infinite;
}


@keyframes text-animation {
    0% {
        transform: translateY(0);
    }

    16.66% {
        transform: translateY(0);
    }

    33.33% {
        transform: translateY(-90px);
    }

    50% {
        transform: translateY(-90px);
    }

    66.66% {
        transform: translateY(-180px);
    }

    83.33% {
        transform: translateY(-180px);
    }

    100% {
        transform: translateY(0);
    }
}
</style>