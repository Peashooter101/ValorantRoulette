<template>
    <div class="main">
      <div class="column">
        <select v-model="selectedGun">
          <option value="" selected disabled>Choose Pistol</option>
          <option v-for="gun in (gunsByName.keys() || [])" :key="gun">{{ gun }}</option>
        </select>
        <div v-if="selectedGun">
          <h1 class="gun-title">{{ selectedGun.toUpperCase() || "No Pistol Selected" }}</h1>
          <div class="gun-info">
            <img v-if="selectedGunJson.displayIcon" class="gun-icon" :src="selectedGunJson.displayIcon"/>
            <div class="gun-details">
              <p>{{ selectedGunJson.displayName || "No Pistol Display Name Present" }}</p><br/>
              <div class="attachment-list">
                <img v-for="attachment in selectedGunJson.attachments" :key="attachment.uuid" class="attachment-icon" :src="attachment.displayIcon || 'https://via.placeholder.com/100'"/>
              </div>
            </div>
          </div>
          <div>
            <h1>Debug Information</h1>
            <p>Selected Pistol: {{ selectedGun || "No Pistol Selected" }}</p>
            <p>Pistol displayIcon: {{ selectedGunJson.displayIcon || "No Pistol Display Icon Present" }}</p>
            <p>Pistol JSON: {{ selectedGunJson || "No Pistol JSON Present" }}</p>
          </div>
        </div>
      </div>
      <div class="column">
        <StrategyRoulette/>
      </div>
    </div>
  </template>
  
  <script setup>
    import { watch, ref } from "vue";
    const gunsEndpoint = "https://valorant-api.com/v1/weapons";
    const gunsByName = ref(new Map());
    const selectedGun = ref("");
    const selectedGunJson = ref(null);
    parseGuns();
  
    async function parseGuns() {
      fetch(gunsEndpoint)
        .then(async (response) => {
          // console.log(await response.text())
          var gunsJson = JSON.parse(await response.text()).data;

          gunsJson.forEach((i) => {
            if (i.shopData.category == "Pistols")
            gunsByName.value.set(i.displayName, i)});

          gunsByName.value = new Map([...gunsByName.value.entries()].sort());
        });
    }
  
    watch(selectedGun, (i) => (selectedGunJson.value = gunsByName.value.get(i)));
  </script>
  
  <style scoped>
  .main {
    display: flex;
    justify-content: space-around;
    margin-top: 60px;
  }
  
  .column {
    min-width: 30vw;
    max-width: 30vw;
  }
  
  .gun-info {
    margin: 20px;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 10px;
    text-align: center;
    box-shadow: 2px 2px 5px #ccc;
  }
  
  .gun-title {
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    font-size: 2em;
    margin-top: 0.2em;
    margin-bottom: 0.2em;
  }
  
  img.gun-icon {
    width: 200px;
    height: 200px;
    margin-top: 20px;
    margin-bottom: 20px;
  }
  
  .gun-stats {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 20px;
    margin-bottom: 20px;
  }
  
  .gun-stat {
    margin-left: 10px;
    margin-right: 10px;
  }
  
  .gun-ability {
    margin-top: 20px;
  }
  
  .gun-ability-title {
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    font-size: 1.5em;
    margin-top: 0.2em;
    margin-bottom: 0.2em;
  }
  
  img.ability-icon {
    width: 100px;
    height: 100px;
    margin: 10px;
  }
  
  .debug-info {
    margin-top: 20px;
  }
  
  h1 {
    margin-top: 20px;
    margin-bottom: 10px;
  }
</style>
