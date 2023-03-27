<template>
    <div v-if="agentsByName.size != 0">
        <select v-model="selectedAgent">
            <option value="" selected disabled>Choose Agent</option>
            <option v-for="agent in (agentsByName.keys() || [])" :key="agent">{{ agent }}</option>
        </select>
        <div v-if="selectedAgent">
            <h1 class="agent-title">{{ selectedAgent.toUpperCase() || "No Agent Selected" }}</h1>
            <div class="agent-info">
                <img v-if="selectedAgentJson.displayIcon" class="agent-icon" :src="selectedAgentJson.displayIcon"/>
                <div class="agent-details">
                    <p>{{ selectedAgentJson.description || "No Agent Description Present" }}</p><br/>
                    <div class="ability-list">
                        <img v-for="ability in selectedAgentJson.abilities" :key="ability" class="ability-icon" :src="ability.displayIcon || 'https://static.wikia.nocookie.net/overwatch_gamepedia/images/5/53/Ability-genji5.png'"/>
                    </div>
                </div>
            </div>
            <div>
                <h1>Debug Information</h1>
                <p>Selected Agent: {{ selectedAgent || "No Agent Selected" }}</p>
                <p>Agent displayIcon: {{ selectedAgentJson.displayIcon || "No Agent Display Icon Present" }}</p>
                <p>Agent JSON: {{ selectedAgentJson || "No Agent JSON Present" }}</p>
            </div>
        </div>
    </div>
    <p v-else>Agents are not yet loaded.</p>
</template>

<script setup>
    import { watch, ref } from 'vue';
    const agentsEndpoint = "https://valorant-api.com/v1/agents";
    const agentsByName = ref(new Map());
    const selectedAgent = ref('');
    const selectedAgentJson = ref(null);
    parseAgents()

    async function parseAgents() {
        fetch(agentsEndpoint + "?isPlayableCharacter=true")
            .then(async response => {
                var agentsJson = JSON.parse(await response.text()).data;
                agentsJson.forEach((i) => agentsByName.value.set(i.displayName, i));
                agentsByName.value = new Map([...agentsByName.value.entries()].sort());
            });
    }

    watch(selectedAgent, (i) => selectedAgentJson.value = agentsByName.value.get(i) )
</script>

<style scoped>
    img.agent-icon {
        width: 200px;
        height: 200px;
    }
    img.ability-icon {
        width: 100px;
        height: 100px;
        margin: 10px;
    }

    .agent-title {
        font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
        font-size: 5em;
        margin-top: 1em;
        margin-bottom: 1em;
    }

    .agent-info {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
    }

    .agent-details {
        min-width: 500px;
        max-width: 35%;
    }

    p.agent-details {
        word-break: normal;
        white-space: normal;
    }

    .ability-list {
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
        justify-content: space-around;
        background-color: black;
        padding:10px;
    }

    body {
        font-family: Arial, Helvetica, sans-serif;
        overflow: hidden;
    }
</style>