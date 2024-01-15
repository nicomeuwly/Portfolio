<script>
import Window from "@/components/Window.vue";
import MainButton from "@/components/mainButton.vue";
import data from "../data.json";

export default {
    name: "JobWindow",
    components: {
        Window,
        MainButton
    },
    props: {
        jobId: Number,
    },
    data() {
        return {
            job: data.jobs[this.jobId],
        };
    },
    methods: {
        receiveDataFromChild(data) {
            this.$emit("parent-to-grandparent", data);
        },
    },
    components: { Window, MainButton }
};
</script>

<template>
    <Window @child-to-parent="receiveDataFromChild">
        <div class="container">
            <div class="left-side">
                <h1>{{ job.title }}</h1>
                <p>{{ job.description }}</p>
                <div class="tags-container">
                    <span v-for="tag in job.tags" :key="tag" class="tag">{{ tag }}</span>
                </div>
            </div>
            <div class="right-side">
                <img :src="'/Portfolio/img/jobs/' + job.image" alt="job image" />
                <MainButton v-for="link in job.links" :key="link.title" :name="link.title" :link="link.url" />
            </div>
        </div>
    </Window>
</template>

<style scoped>
h1,
p {
    color: var(--white);
    margin: 0;
}

.container {
    display: flex;
    flex-direction: row;
    gap: 30px;
    height: 100%;
    width: 100%;
}

.left-side {
    display: flex;
    flex-direction: column;
    gap: 30px;
    width: 50%;

}

.right-side {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    gap: 30px;
    width: 50%;
    height: 100%;
}
.tags-container {
    display: flex;
    gap: 10px;
}
.tag {
    background-color: var(--white-2);
    color: var(--white);
    border-radius: 10px;
    padding: 10px;
}
img {
    max-width: 100%;
    max-height: 60%;
}
MainButton {
    width: 50%;
}
</style>
