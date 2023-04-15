<template>
  <div class="main">
    <BackgroundVideo/>
    <div class="column">
      <AgentInfo/>
    </div>
    <div class="column">
      <GunUwW/>
    </div>
    <div class="column">
      <StrategyRoulette/>
    </div>
  </div>
</template>

<script>
import AgentInfo from './components/AgentInfo.vue';
import BackgroundVideo from './components/BackgroundVideo.vue';
import StrategyRoulette from './components/StrategyRoulette.vue';
import GunUwW from './components/GunUwW.vue';

export default {
  name: 'App',
  components: {
    BackgroundVideo,
    AgentInfo,
    StrategyRoulette,
    GunUwW
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
