<template>
    <div>
        <ul>
            <li v-bind:key="gif.id" v-for="gif in gifs">
                <img :src="gif.images.fixed_height.url" />
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: ['gifs']
}
//You can use v-bind:src instead of :src
</script>

<style>
li {
    display: inline;
}
</style>
