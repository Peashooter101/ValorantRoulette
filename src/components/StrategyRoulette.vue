<template>
    <button @click="randomize">Randomize Strategy</button>
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

    function randomize() {
        strategy.value = strats[Math.floor(Math.random() * strats.length)];
    }

    function parseDescription(desc) {
        desc = replaceEcoRanges(desc);
        return desc;
    }

    function replaceEcoRanges(str) {
        const rangeReplace = str.match(/\{ecoRange-\d+-\d+\}/) || [];
        rangeReplace.forEach(range => {
            const rangeInfo = range.split('-');
            const rangeMax = rangeInfo[2].substring(0,rangeInfo[2].length-1) / 50;
            const rangeMin = rangeInfo[1] / 50;
            const result = Math.round(Math.random() * (rangeMax - rangeMin) + rangeMin);
            str = str.replace(range, result * 50);
        })
        return str;
    }
</script>

<style scoped>
</style>