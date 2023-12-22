<template>
  <div class="topnav">
    <button @click="currentWindow = Page.AgentInfo">Agent Info</button>
    <button @click="currentWindow = Page.WeaponInfo">Weapon Info</button>
    <button @click="currentWindow = Page.StrategyRoulette">Strategy Roulette</button>
  </div>
  <div class="main">
    <BackgroundVideo/>
    <div class="window">
      <AgentInfo v-if="currentWindow === Page.AgentInfo"/>
      <GunUwW v-if="currentWindow === Page.WeaponInfo"/>
      <StrategyRoulette v-if="currentWindow === Page.StrategyRoulette"/>
    </div>
  </div>
</template>

<script>
import AgentInfo from './components/AgentInfo.vue';
import BackgroundVideo from './components/BackgroundVideo.vue';
import StrategyRoulette from './components/StrategyRoulette.vue';
import GunUwW from './components/GunUwW.vue';

const Page = Object.freeze({
  AgentInfo: Symbol("AgentInfo"),
  StrategyRoulette: Symbol("StrategyRoulette"),
  WeaponInfo: Symbol("WeaponInfo")
})

export default {
  name: 'App',
  components: {
    BackgroundVideo,
    AgentInfo,
    StrategyRoulette,
    GunUwW
  },
  data() {
    return {
      currentWindow: Page.AgentInfo,
      Page
    };
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
</style>
