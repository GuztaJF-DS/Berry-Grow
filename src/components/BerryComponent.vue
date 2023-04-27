<script setup lang="ts">
import type { IBerryCollection } from '@/views/HomeView.vue';
import { toRefs, ref } from 'vue';

const currentItem = defineProps<{item: IBerryCollection }>();
const currentBerry = ref(toRefs(currentItem.item.berry));
let currentAnimationFrame = ref(1);
let animationKeyFrame = false;

function getAnimationFrame(){
  if(currentItem.item.currentPhase===0){
    animationKeyFrame =false;
  }
  setTimeout(() => {
    animationKeyFrame=!animationKeyFrame;
    currentAnimationFrame.value = animationKeyFrame ? 1 : 2;

    getAnimationFrame();
  }, 500);
};

getAnimationFrame();
</script>

<template>
  <div class="berry">
    <img 
      draggable="false"
      :src="'src/assets/sprites/' + 
        currentBerry.sprites[currentItem.item.currentPhase]
      + currentAnimationFrame + '.svg'"
    >
      {{ currentItem.item.timePassed }}
  </div>  
</template>

<style scoped>

.berry > img {
  bottom: 40px
}

.berry:hover {
  background-color: red;
}
</style>