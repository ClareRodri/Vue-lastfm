<template>
    <li>
        <h2><a v-bind:href="artist.url">{{artist.name}}</a></h2>
            <img v-bind:src="artist.image[2]['#text']">
        
    </li>
</template>

<script>
export default {
    name: 'artist',
    props: ['artist']
}
</script>

<style>
li {
    display: block;
    margin: 10px 0;
}
</style>
