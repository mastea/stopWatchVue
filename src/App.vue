<script setup>
import { ref } from "vue";

let id = 1;
const sWatches = ref([
  { id: id++, time: 3734, running: false, interval: null },
  { id: id++, time: 13, running: false, interval: null }
]);

const startBtn = (watch) => {
  if (!watch.running) {
    watch.running = true;
    watch.interval = setInterval(() => {
      watch.time++;
    }, 1000);
  }
};
const pauseBtn = (watch) => {
  watch.running = false;
  clearInterval(watch.interval);
};
const stopBtn = (watch) => {
  watch.running = false;
  clearInterval(watch.interval);
  watch.time = 0;
};
const addNew = () => {
  sWatches.value.push({ id: id++, time: 0, running: false, interval: null });
}
</script>
<template>
  <div class="wrapper">
    <ul>
      <li v-for="watch in sWatches" :key="watch.id">
        <span id="text">
          {{
            (parseInt(parseInt(watch.time / 60) / 60) % 60).toLocaleString(undefined, { minimumIntegerDigits: 2 })
          }}.{{
            (parseInt(watch.time / 60) % 60).toLocaleString(undefined, { minimumIntegerDigits: 2 })
          }}.{{
            (watch.time % 60).toLocaleString(undefined, { minimumIntegerDigits: 2 })
          }}
        </span>
        <img id="line" src="./assets/svg/vector.svg" />
        <img :class="{ hide: watch.running }" @click="startBtn(watch)" id="play" src="./assets/svg/play.svg" />
        <img :class="{ hide: !watch.running }" @click="pauseBtn(watch)" id="pause" src="./assets/svg/pause.svg" />
        <img @click="stopBtn(watch)" id="stop" src="./assets/svg/stop.svg" />
      </li>
      <li>
        <img @click="addNew" id="addNew" src="./assets/svg/add.svg" />
      </li>
    </ul>
  </div>
</template>
<style scoped>
  .hide {
    display: none;
  }
</style>
