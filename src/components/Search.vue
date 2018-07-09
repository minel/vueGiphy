<template>
    <div class="search">
        <input v-on:keypress.enter="requestSearch" type="text" v-model="query" />
        <button @click="requestSearch">Search</button>
    </div>
</template>

<script>
//You can use @ (at) sign instead of 'v-on:' notation
export default {
    data() {
        return {
            query: ''
        }
    },
    methods: {
        requestSearch() {
            this.$emit('SearchRequested', this.query);
            console.log('requestSearch: ', this.query ? this.query : '<empty>');
        }
    }
}
</script>
<style>
    .search input {
        padding: 10px 20px;
        border: 1px solid;
        border-radius: 5px;
        width: 400px;
    }

    .search button {
        padding: 5px 15px;
        border: 1px solid #ccc;
        background-color: #4183c4;
        color: #fff;
        border-radius: 5px;
    }
</style>
