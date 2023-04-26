<script setup lang="ts">
import { ref } from 'vue';
const items = ref([{ name: 'Aspear', count: 0 }, { name: 'Aspear', count: 0 }]);

function startClock() {
  setTimeout(() => {
    items.value.map((item)=>{
      return item.count+=1;
    })
    startClock()
  }, 1000)
}

function resetClock(index: number) {
  items.value[index].count = 0;
}
startClock();
</script>

<template>
  <div class="land">
    <img draggable="false" src="../assets/sprites/general/dirt.svg">
    <div class="berryBox">
      <div class="berry" @click="resetClock(index)"  v-for="(item, index) in items" :key="index">
        <img draggable="false" src="../assets/sprites/general/plantedDirt.png">
        {{ item.count }}
      </div>
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

  .berry > img {
    bottom:40px
  }
  .berry:hover {
    background-color: red;
  }
</style>
