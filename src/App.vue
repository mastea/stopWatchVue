<script setup>
import { ref } from "vue";

const sWatches = ref([]);
const running = ref(false);
const interval = ref(null);

const hours = ref(0);
const minutes = ref(0);
const seconds = ref(0);
const time = ref(0);

const startBtn = () => {
  if (!running.value) {
    running.value = true;
    interval.value = setInterval(() => {
      time.value++;
      seconds.value = time.value;
      minutes.value = parseInt(seconds.value / 60);
      hours.value = parseInt(minutes.value / 60);
      console.log(time.value);
    }, 1000);
  }
};
const pauseBtn = () => {
  running.value = false;
  clearInterval(interval.value);
};
const stopBtn = () => {
  running.value = false;
  clearInterval(interval.value);
  time.value = 0;
  seconds.value = 0;
  minutes.value = 0;
  hours.value = 0;
};
const addNew = () => {
  
}
</script>
<template>
  <div class="wrapper">
    <ul>
      <li>
        <span id="text">
          {{ hours.toLocaleString(undefined, { minimumIntegerDigits: 2 }) }}.{{
            (minutes % 60).toLocaleString(undefined, {
              minimumIntegerDigits: 2,
            })
          }}.{{
            (seconds % 60).toLocaleString(undefined, {
              minimumIntegerDigits: 2,
            })
          }}
        </span>
        <img id="line" src="./assets/svg/vector.svg" />
        <img :class="{ hide: running }" @click="startBtn" id="play" src="./assets/svg/play.svg" />
        <img :class="{ hide: !running }" @click="pauseBtn" id="pause" src="./assets/svg/pause.svg" />
        <img @click="stopBtn" id="stop" src="./assets/svg/stop.svg" />
      </li>
      <li>
        <img @click="addNew" id="add" src="./assets/svg/add.svg" />
      </li>
    </ul>
  </div>
</template>
<style scoped>
  .hide {
    display: none;
  }
</style>