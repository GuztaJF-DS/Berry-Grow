<script setup lang="ts">
import { ref } from 'vue';
import BerryComponent from '../components/BerryComponent.vue';

export interface IBerryCollection {
  berry: IBerry,
  timePassed: number,
  currentPhase: number,
}

export interface IBerry {
  name: string,
  growthPhases: string[],
  sprites: string[],
  yieldMin: number,
  yieldMax: number
}

const individualBerry: IBerry = {
  name: 'Aspear',
  growthPhases:[
    '0',
    '10',
    '20',
    '30',
    '40'
  ],
  sprites:[
    'general/plantedDirt',
    'general/bud',
  ],
  yieldMin:1,
  yieldMax:2,
}

const items = ref<IBerryCollection[]>([
  { berry: individualBerry, timePassed: 0, currentPhase: 1 },
  { berry: individualBerry, timePassed: 0, currentPhase: 0 },
]);


function startClock() {
  setTimeout(() => {
    items.value.map((item) => {
      return item.timePassed += 1;
    })
    startClock()
  }, 1000)
}

function resetClock(index: number) {
  items.value[index].timePassed = 0;
}
startClock();
</script>

<template>
  <div class="land">
    <img draggable="false" src="../assets/sprites/general/dirt.svg">
    <div class="berryBox">
      <BerryComponent 
        v-for="(item, index) in items"
        :key="index" @click="resetClock(index)"
        :item=item 
      />
    </div>
  </div>
</template>

<style scoped>
  .land{
    align-self: center;
  }

  .berryBox{
    position: absolute;
    left: 19px;
    bottom:21px;
    display: grid;
    grid-template-columns: 48px 48px;
    grid-column-gap: 11px;
    grid-auto-rows: 48px;
  }
</style>
