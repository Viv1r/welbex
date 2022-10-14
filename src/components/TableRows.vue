<template>
    <div class="table__body">
        <div class="table__row" v-for="row of data">
            <div
                v-for="(item, key) in pattern"
                class="table__cell"
                :key="key"
            >
                {{ row[key] }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        data: {
            type: Array,
            default: []
        },
        pattern: {
            type: Object,
            default: []
        },
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
        transition: all .15s ease-out;
    }

    .table__row:hover {
        background-color: rgba(0, 0, 0, .12);
    }

    .table__cell {
        display: flex;
        padding: 16px 12px 16px 12px;
        text-align: start;
        word-break: break-word;
    }
</style>