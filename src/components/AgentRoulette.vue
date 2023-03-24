<template>
    <p v-if="agentsByName">{{ agentsByName }}</p>
    <p v-else>hi</p>
</template>

<script setup>
    /* eslint-disable */
    import { ref } from 'vue';
    const agentsEndpoint = "https://valorant-api.com/v1/agents";
    const agentsByName = ref(new Map());
    setTimeout(async () => await parseAgents(), 5000);

    async function parseAgents() {
        fetch(agentsEndpoint + "?isPlayableCharacter=true")
            .then(async r => {
                var agentsJson = JSON.parse(await r.text()).data;
                agentsJson.forEach((i) => agentsByName.value.set(i.displayName, i.uuid));
            });
        console.log(agentsByName.value);
    }
</script>

<style scoped>

</style>