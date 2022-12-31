<script setup lang="ts">
import Progress from "../lib/Progress.vue";
import { ref } from "vue";

const percents = [ref(50), ref(40), ref(30), ref(20)];

function update(p: typeof percents[0]) {
  if (p.value >= 100) {
    return;
  }

  setTimeout(() => {
    p.value++;

    update(p);
  }, 50);
}

percents.forEach(update);
</script>

<template>
  <Progress
    :percent="percents[0].value"
    colors="#52c41a 0%, #eb2f96 40%, #1677ff 80%, #52c41a 100%"
  />
  <br />
  <Progress
    :percent="percents[1].value"
    timing-func="ease"
    colors="#52c41a 0%, #95de64 40%, #d9f7be 80%, #52c41a 100%"
  />
  <br />
  <Progress
    :percent="percents[2].value"
    timing-func="ease-in"
    colors="#1677ff 0%, #69b1ff 40%, #bae0ff 80%, #1677ff 100%"
  />
  <br />
  <Progress
    :percent="percents[3].value"
    timing-func="ease-out"
    colors="#eb2f96 0%, #ff85c0 40%, #ffd6e7 80%, #eb2f96 100%"
  />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
