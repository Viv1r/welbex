<template>
    <div class="container">
        <div class="table">
            <Filter
                :pattern="pattern"
                :filterBy="filterBy"
                @sortBy="(value) => sortBy = value"
                @filterBy="(key, value) => {
                    if (key === 'field' && !value)
                        filterBy = {};
                    filterBy[key] = value;
                }"
            />
            <TableHead
                :pattern="pattern"
            />
            <TableRows
                :data="readyData.slice((currentPage-1)*rowsPerPage, currentPage*rowsPerPage)"
                :pattern="pattern"
            />
            <Pagination
                :pagesCount="pagesCount"
                :currentPage="currentPage"
                @setPage="(val) => currentPage = val"
            />
        </div>
    </div>
</template>

<script>
import MainData from './data/MainData.json' assert {type: 'json'};
import TableHead from "./components/TableHead.vue";
import TableRows from "./components/TableRows.vue";
import Pagination from "./components/Pagination.vue";
import Filter from "./components/Filter.vue";

export default {
    components: {
        TableHead,
        TableRows,
        Pagination,
        Filter
    },
    created() {
        if (!Array.isArray(this.rawData)) {
            this.rawData = [];
            console.log('Wrong data!');
        }
    },
    data() {
        return {
            rawData: MainData,
            currentPage: 1,
            rowsPerPage: 10,
            sortBy: null,
            filterBy: {},
            pattern: {
                date: {
                    title: 'Дата',
                    sortingAllowed: false
                },
                title: {
                    title: 'Название',
                    sortingAllowed: true
                },
                count: {
                    title: 'Количество',
                    sortingAllowed: true
                },
                distance: {
                    title: 'Расстояние',
                    sortingAllowed: true
                }
            }
        }
    },
    computed: {
        readyData: function() {
            this.currentPage = 1;

            const sortBy = this.sortBy,
                  filterBy = this.filterBy;

            const tempData = (() => {
                if (sortBy === 'default' || !sortBy || !this.pattern[sortBy] || !this.pattern[sortBy].sortingAllowed) {
                    return this.rawData;
                }
                return [...this.rawData].sort((a, b) => {
                    a = a[sortBy];
                    b = b[sortBy];
                    if (typeof(a) === 'string')
                        a = a.toLowerCase();
                    if (typeof(b) === 'string')
                        b = b.toLowerCase();
                    if (a > b) return 1;
                    if (a < b) return -1;
                    return 0;
                });
            })();

            const [field, operator, value] = [filterBy.field, filterBy.operator, filterBy.value];
            if (typeof(filterBy) !== 'object' || !(field && operator && value)) return tempData;

            switch (operator) {
                case '>':
                    return tempData.filter(elem => Number(elem[field]) > value);
                case '<':
                    return tempData.filter(elem => Number(elem[field]) < value);
                case '=':
                    return tempData.filter(elem => elem[field] == value);
                case '^':
                    return tempData.filter(elem => String(elem[field]).includes(value));
                default:
                    return tempData;
            }
        },
        pagesCount: function() {
            return Math.ceil(this.readyData.length/this.rowsPerPage);
        }
    }
}
</script>

<style scoped>
    .container {
        width: auto;
        min-width: 800px;
        max-width: 1400px;
        height: fit-content;
        display: block;
        margin: auto;
    }
</style>
