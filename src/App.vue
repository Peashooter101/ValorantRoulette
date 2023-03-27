<template>
  <div class="main">
    <div class="column">
      <AgentRoulette/>
    </div>
    <div class="column">
      <AgentRoulette/>
    </div>
    <div class="column">
      <AgentRoulette/>
    </div>
  </div>
</template>

<script>
import AgentRoulette from './components/AgentRoulette.vue'

export default {
  name: 'App',
  components: {
    AgentRoulette
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.main {
  display: flex;
  justify-content: space-around;
}

.column {
  min-width: 30vw;
  max-width: 30vw;
}
</style>
