<template>
    <div class="container">
        <div class="table">
            <TableHeader/>
            <TableRows
                :sortedData="sortedData"
            />
            <Pagination
                :pagesCount="5"
            />
        </div>
    </div>
</template>

<script>
import { RouterLink, RouterView } from 'vue-router';
import MainData from './data/MainData.json' assert {type: 'json'};
import TableHeader from "./components/TableHeader.vue";
import TableRows from "./components/TableRows.vue";
import Pagination from "./components/Pagination.vue";

export default {
    components: {
        TableHeader,
        TableRows,
        Pagination
    },
    data() {
        return {
            tableData: MainData
        }
    },
    computed: {
        sortedData: function() {
            return this.tableData;
        }
    },
    created() {
        if (!Array.isArray(this.tableData)) {
            this.tableData = [];
            console.log('Wrong data!');
        }
    }
}
</script>

<style scoped>
    .container {
        width: auto;
        min-width: 400px;
        max-width: 1200px;
        height: fit-content;
        display: block;
        margin: auto;
    }
</style>
