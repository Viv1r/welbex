<template>
    <div class="table__body">
        <div class="table__row" v-for="row of sortedData">
            <div v-for="title of pattern" class="table__cell">
                {{ row[title] }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            pattern: [
                'date',
                'title',
                'count',
                'distance'
            ]
        }
    },
    props: {
        sortedData: {
            type: Array,
            default: []
        }
    }
}
</script>

<style scoped>
    .table__body {
        width: 100%;
        height: fit-content;
        display: flex;
        flex-direction: column;
    }

    .table__row {
        width: 100%;
        height: auto;
        min-height: 64px;
        display: grid;
        grid-template-columns: 25% 25% 25% 25%;
        background-color: #e8e8e8;
    }

    .table__row:hover {
        background-color: rgba(0, 0, 0, .12);
    }

    .table__cell {
        display: flex;
        align-items: center;
        padding: 12px;
        text-align: start;
        word-break: break-word;
    }
</style>