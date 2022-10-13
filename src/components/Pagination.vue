<template>
    <div class="pagination">
        <div
            v-for="index in pagesCount"
            class="page_link"
        >{{ index }}</div>
    </div>
</template>

<script>
export default {
    props: {
        pagesCount: {
            type: Number,
            default: 0
        }
    }
}
</script>

<style scoped>
    .pagination {
        width: 100%;
        height: auto;
        padding: 8px;
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 8px;
        background-color: #dadada;
    }
    .page_link {
        font-weight: bold;
        cursor: pointer;
    }
    .page_link:hover {
        color: purple;
    }
</style>