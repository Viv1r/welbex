<template>
    <div class="pagination">
        <div
            v-for="index in pagesCount"
            class="page_link"
            v-bind:class="{
                selected: currentPage === index
            }"
            v-on:click="$emit('setPage', index)"
        >{{ index }}</div>
    </div>
</template>

<script>
export default {
    props: {
        pagesCount: {
            type: Number,
            default: 1
        },
        currentPage: {
            type: Number,
            default: 1
        }
    },
    emits: [
        'setPage'
    ]
}
</script>

<style scoped>
    .pagination {
        width: 100%;
        height: auto;
        min-height: 48px;
        padding: 8px;
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
        gap: 8px;
        background-color: #dadada;
    }

    .page_link {
        transition: all .2s ease-out;
        font-weight: bold;
        cursor: pointer;
    }

    .page_link:hover {
        font-size: 1.1rem;
    }

    .page_link.selected {
        color: purple;
    }
</style>