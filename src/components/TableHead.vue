<template>
    <div class="table__head">
        <div
            v-for="(item, key) in pattern"
            @click="sortBy(key)"
            class="column_header"
            :key="key"
        >
            {{ item.title }}
        </div>
    </div>
</template>

<script>
export default {
    props: {
        pattern: {
            type: Object,
            default: {}
        }
    },
    created() {
    },
    methods: {
        sortBy(header) {
            if (header.sortingAllowed) {
                console.log('Sorting!');
            }
        }
    }
}
</script>

<style scoped>
    .table__head {
        width: 100%;
        height: 64px;
        background-color: #6b6b6b;
        color: white;
        display: grid;
        grid-template-columns: 25% 25% 25% 25%;
    }

    .column_header {
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
        transition: all .1s ease-out;
        cursor: pointer;
    }

    .column_header:hover {
        background-color: rgba(0, 0, 0, .05);
    }
</style>