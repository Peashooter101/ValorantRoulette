<template>
    <!-- Borrowing BG Video from https://schoch.co.nz/valorant (TODO: Change)-->
    <video id="background-video" playsinline autoplay muted loop>
        <source src="https://schoch.co.nz/img/vid.webm" type="video/webm">
    </video>
</template>

<script setup>
</script>

<style scoped>
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