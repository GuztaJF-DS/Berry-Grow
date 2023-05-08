<script setup lang="ts">
import { ref, inject } from 'vue';
import type { VueCookies } from 'vue-cookies'
import BerryComponent from '../components/BerryComponent.vue';
const $cookies = inject<VueCookies>('$cookies');

export interface IBerryCollection {
  berryId: string,
  berry: IBerry,
  timePassed: number,
  currentPhase: number,
}

export interface IBerry {
  name: string,
  growthPhases: number[],
  sprites: string[],
  yieldMin: number,
  yieldMax: number
}

const AspearBerry: IBerry = {
  name: 'Aspear',
  growthPhases:[
    10,
    20,
    30,
    40
  ],
  sprites:[
    'general/plantedDirt',
    'general/bud',
    'aspear/tall/aspear',
    'aspear/flower/aspear',
    'aspear/grown/aspear',
  ],
  yieldMin:2,
  yieldMax:3,
}

const items = ref<IBerryCollection[]>([
  { berryId:'AspearBerry', berry: AspearBerry, timePassed: 0, currentPhase: 0 },
  { berryId: 'AspearBerry', berry: AspearBerry, timePassed: 10, currentPhase: 1 },
]);


function startClock() {
  if($cookies){
    const preStoredBerries = $cookies.get('berry');
    if(!preStoredBerries){
      $cookies.set('berry', items);
      console.log('preStoredBerries')
    }
    console.log(preStoredBerries._value)
  }
  advanceClock()
}


function advanceClock() {
  setTimeout(() => {
    items.value.map((item) => {
      if (item.berry.growthPhases[item.currentPhase] === item.timePassed + 1) {
        item.currentPhase += 1;
      }
      return item.timePassed += 1;
    })
    advanceClock()
  }, 1000)
}

function resetClock(index: number) {
  items.value[index].timePassed = 0;
  items.value[index].currentPhase = 0;
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
    grid-template-columns: repeat(4,48px);
    grid-column-gap: 11px;
    grid-auto-rows: 48px;
  }
</style>
