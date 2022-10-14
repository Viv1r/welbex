<template>
    <div class="menu">
        <div class="sorting__wrapper">
            <img src="../assets/sort.svg" alt="sort">
            <select
                class="sorting__selector"
                @change="$emit('sortBy', $event.target.value)"
            >
                <option value="default">По умолчанию</option>
                <template v-for="(item, key) in pattern">
                    <option
                        v-if="item.sortingAllowed"
                        :value="key"
                        :key="key"
                    >
                        {{ item.title }}
                    </option>
                </template>
            </select>
        </div>
        <div class="filtering__wrapper">
            <img src="../assets/filter.svg" alt="filter">
            <select
                class="filtering__selector__field"
                @change="$emit('filterBy', 'field', $event.target.value)"
            >
                <option value="">Без фильтра</option>
                <option
                    v-for="(item, key) in pattern"
                    :value="key"
                    :key="key"
                >{{ item.title }}</option>
            </select>
            <template v-if="filterBy.field">
                <select
                    class="filtering__selector__operator"
                    @change="$emit('filterBy', 'operator', $event.target.value)"
                >
                    <option value=""></option>
                    <option
                        v-for="item of operators"
                        :value="item.tag"
                        :key="item.tag"
                    >{{ item.title }}</option>
                </select>
                <input
                    type="text"
                    class="filtering__selector__value"
                    @input="$emit('filterBy', 'value', $event.target.value)"
                >
            </template>
        </div>
    </div>
</template>

<!-- Прошу прощения за корявый нейминг :) -->

<script>
export default {
    data() {
        return {
            operators: [
                {
                    title: 'Больше',
                    tag: '>'
                },
                {
                    title: 'Меньше',
                    tag: '<'
                },
                {
                    title: 'Равно',
                    tag: '='
                },
                {
                    title: 'Содержит',
                    tag: '^'
                }
            ]
        }
    },
    props: {
        pattern: {
            type: Object,
            default: []
        },
        filterBy: {
            type: Object,
            default: {}
        }
    },
    emits: [
        'sortBy',
        'filterBy'
    ]
}
</script>

<style scoped>
    .menu {
        width: 100%;
        height: 48px;
        display: flex;
        flex-direction: row;
        background-color: #4b4b4b;
    }

    .filtering__wrapper,
    .sorting__wrapper {
        width: fit-content;
        padding: 0px 8px 0px 8px;
        display: flex;
        flex-direction: row;
        gap: 16px;
        align-items: center;
    }

    img {
        filter: invert(100%);
        width: 40px;
        height: 40px;
    }

    select, input {
        width: auto;
        min-width: 140px;
        height: 26px;
        border: none;
        background-color: #c0c0c0;
    }
</style>