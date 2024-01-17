<script>
import Window from "@/components/Window.vue";

export default {
    name: "LandingWindow",
    components: {
        Window,
    },
    data() {
        return {
            typeValue: "",
            typeStatus: false,
            displayTextArray: ["Développeur web", "Designer UI", "Gamer..."],
            typingSpeed: 100,
            erasingSpeed: 100,
            newTextDelay: 2000,
            displayTextArrayIndex: 0,
            charIndex: 0,
        };
    },
    methods: {
        receiveDataFromChild(data) {
            this.$emit("parent-to-grandparent", data);
        },
        typeText() {
            if (this.charIndex < this.displayTextArray[this.displayTextArrayIndex].length) {
                if (!this.typeStatus) this.typeStatus = true;
                this.typeValue += this.displayTextArray[this.displayTextArrayIndex].charAt(
                    this.charIndex
                );
                this.charIndex += 1;
                setTimeout(this.typeText, this.typingSpeed);
            } else {
                this.typeStatus = false;
                setTimeout(this.eraseText, this.newTextDelay);
            }
        },
        eraseText() {
            if (this.charIndex > 0) {
                if (!this.typeStatus) this.typeStatus = true;
                this.typeValue = this.displayTextArray[this.displayTextArrayIndex].substring(
                    0,
                    this.charIndex - 1
                );
                this.charIndex -= 1;
                setTimeout(this.eraseText, this.erasingSpeed);
            } else {
                this.typeStatus = false;
                this.displayTextArrayIndex += 1;
                if (this.displayTextArrayIndex >= this.displayTextArray.length)
                    this.displayTextArrayIndex = 0;
                setTimeout(this.typeText, this.typingSpeed + 1000);
            }
        },
        setBubbleTipPosition() {
            const bubbleWidth = this.$refs.bubble.offsetWidth;
            const tip = this.$refs.tip;
            const tipWidth = tip.offsetWidth;
            tip.style.left = `${bubbleWidth - tipWidth * 0.7}px`;
            tip.style.top = `${-tipWidth * 0.7}px`;
        },
    },
    created() {
        setTimeout(this.typeText, this.newTextDelay + 100);
    },
    mounted() {
        this.setBubbleTipPosition();
        window.addEventListener("resize", this.setBubbleTipPosition);
    },
};
</script>

<template>
    <Window @child-to-parent="receiveDataFromChild">
        <div id="landing-window-content">
            <div id="left-side">
                <p>Nicolas Meuwly</p>
                <div id="bubble-container" ref="bubble">
                    <span class="typed-text">{{ typeValue }}</span>
                    <span class="blinking-cursor">|</span>
                    <span class="cursor" :class="{ typing: typeStatus }">&nbsp;</span>
                </div>
                <img src="/img/Tip.svg" id="bubble-tip" alt="Bubble tip" ref="tip"/>
            </div>
            <div id="right-side">
                <img src="/img/Avatar.png" id="avatar" />
            </div>
        </div>
    </Window>
</template>

<style lang="scss" scoped>
#landing-window-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    height: 100%;
}

#avatar {
    height: 70%;
    aspect-ratio: 1/1;
    border-radius: 50%;
    border: 2px solid var(--white);
    background-color: var(--blue-2);
}

#left-side>p {
    color: var(--white);
    font-size: 2rem;
    margin-bottom: 0.5em;
}

#left-side {
    width: 45%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
}

#right-side {
    width: 45%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: flex-end;
}

#bubble-container {
    background-color: var(--white);
    border-radius: 20px;
    display: flex;
    align-items: center;
    width: 100%;
    height: 20%;
}
#bubble-tip {
    width: 15%;
    position: relative;
}

.blinking-cursor {
    font-size: 2.3rem;
    margin-bottom: 0.5rem;
    color: var(--black);
    -webkit-animation: 1s blink step-end infinite;
    -moz-animation: 1s blink step-end infinite;
    -ms-animation: 1s blink step-end infinite;
    -o-animation: 1s blink step-end infinite;
    animation: 1s blink step-end infinite;
}

.typed-text {
    margin-left: 1rem;
    font-size: 2rem;
    color: var(--blue);
    font-weight: bold;
}

@keyframes blink {

    from,
    to {
        color: transparent;
    }

    50% {
        color: var(--black);
    }
}

@-moz-keyframes blink {

    from,
    to {
        color: transparent;
    }

    50% {
        color: var(--black);
    }
}

@-webkit-keyframes blink {

    from,
    to {
        color: transparent;
    }

    50% {
        color: var(--black);
    }
}

@-ms-keyframes blink {

    from,
    to {
        color: transparent;
    }

    50% {
        color: var(--black);
    }
}

@-o-keyframes blink {

    from,
    to {
        color: transparent;
    }

    50% {
        color: var(--black);
    }
}
</style>