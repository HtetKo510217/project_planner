<template>
  <nav class="filter-nav">
    <button @click="filterBy('all')" :class="{active:current==='all'}">All</button>
    <button @click="filterBy('complete')" :class="{active:current==='complete'}">Complete</button>
    <button @click="filterBy('ongoing')" :class="{active:current==='ongoing'}">Ongoing</button>
  </nav>
</template>

<script>
export default {
    props:['current'],
    methods: {
        filterBy(value) {
            this.$emit('filterValue',value)
        }
    }
}
</script>

<style>
    .filter-nav button {
        margin-right: 10px;
        background: none;
        border: none;
        font-size: 16px;
    }
    .filter-nav .active {
        font-weight: bold;
    }
</style>