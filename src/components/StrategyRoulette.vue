<template>
    <!-- Borrowing BG Video from https://schoch.co.nz/valorant (TODO: Change)-->
    <video id="background-video" playsinline autoplay muted loop>
        <source src="https://schoch.co.nz/img/vid.webm" type="video/webm">
    </video>
    <div>
        <h1>{{ strategy.name }}</h1>
        <p>{{ parseDescription(strategy.description) }}</p>
        <p>{{ strategy.flags }}</p>
    </div>
</template>

<script setup>
    import strategiesYml from '@/assets/strategies.yml';
    import { ref } from 'vue';
    const strats = strategiesYml.strategies;
    const strategy = ref(strats[Math.floor(Math.random() * strats.length)]);

    function parseDescription(desc) {
        desc
    }
</script>

<style>
    #background-video {
        object-fit: cover;
        width: 100%;
        height: 100%;
        position: fixed;
        top: 0;
        left: 0;
        z-index: -99;
    }
</style>