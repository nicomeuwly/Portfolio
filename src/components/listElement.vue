<script>
export default {
    name: "ListElement",
    props: {
        id: Number,
        idName: String,
        title: String,
        date: String,
        description: String,
    },
};
</script>

<template>
    <div id="`${idName}-${id}`" class="list-element">
        <span class="list-element-date">{{ date }}</span>
        <svg>
            <circle class="list-element-circle" cx="50%" cy="50%" r="48%" stroke="white" stroke-width="2%" fill="rgba(0, 2, 41)"/>
        </svg>
        <div class="list-element-content">
            <span class="list-element-title">{{ title }}</span>
            <span class="list-element-description">{{ description }}</span>
        </div>
    </div>
</template>

<style scoped>
    .list-element {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: left;
        gap: 3%;
        width: 100%;
    }
    svg {
        width: 8%;
        aspect-ratio: 1 / 1;
    }
    .list-element-content {
        display: flex;
        flex-direction: column;
        align-items: left;
        justify-content: left;
        gap: 10px;
    }
    span {
        color: var(--white);
    }
    .list-element-title {
        font-size: 2rem;
        font-weight: bold;
    }
    .list-element-date {
        font-size: 1.5rem;
        width: 13%;
        text-align: right;
    }
    .list-element-description {
        font-size: 1rem;
    }
</style>