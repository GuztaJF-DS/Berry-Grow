<script setup lang="ts">
import { ref } from 'vue';
const items = ref([{ message: 'aspear' }, { message: 'Bar' }]);
const state = ref({ count: false })

function reverse(randomData:any) {
  console.log(randomData)
  state.value.count=!state.value.count
}
</script>

<template>
  <div class="land">
    <img draggable="false" src="../assets/dirt.svg">
    <div class="berryBox">
      <div class="berry" @click="reverse(item)" v-for="item in items" :key="item.message">
        <img draggable="false" src="../assets/aspear.svg">
        {{ state.count }}
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
    left: 17px;
    bottom:20px;
    display: grid;
    grid-template-columns: 48px 48px;
    grid-column-gap: 10px;
    grid-auto-rows: 48px;
  }

  .berry > div {
    bottom:40px;
  }

  .berry > img {
    bottom:40px
  }
  .berry:hover {
    background-color: red;
  }
</style>
