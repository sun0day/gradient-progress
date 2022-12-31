<script lang="ts">
export default {
  name: "GradientProgress",
};
</script>

<script setup lang="ts">
const { percent, className, duration, timingFunc, colors, angle } =
  defineProps<{
    percent?: number;
    className?: string;
    duration?: number;
    timingFunc?: string;
    colors?: string;
    angle?: number;
    hideLabel?: boolean;
  }>();
</script>

<template>
  <div
    class="gradient-progress"
    :class="{ [className || '']: !!className }"
    :style="{
      '--progress-gradient': `linear-gradient(${angle || 90}deg, ${
        colors || '#1677ff 0%, #69b1ff 40%, #bae0ff 80%, #1677ff 100%'
      })`,
      '--progress-percent': `${percent || 0}%`,
      '--progress-duration': `${duration || 15}s`,
      '--progress-timing-func': timingFunc || 'linear',
    }"
  >
    <div class="gradient-progress-bar"></div>
    <div v-if="!hideLabel" class="gradient-progress-label">{{ percent }}%</div>
  </div>
</template>

<style scoped>
.gradient-progress {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.gradient-progress .gradient-progress-bar {
  flex: 1;
  height: 8px;
  position: relative;
  border-radius: 10px;
  background: #f5f5f5;
  background-size: 500%;
}

.gradient-progress .gradient-progress-bar::before {
  content: "";
  position: absolute;
  inset: 0;
  width: var(--progress-percent);
  border-radius: 10px;
  background: var(--progress-gradient);
  background-size: 500%;
  animation: loading var(--progress-duration) var(--progress-timing-func)
    infinite;
}

.gradient-progress .gradient-progress-label {
  width: 2em;
  margin-left: 6px;
  color: #212724;
}

@keyframes loading {
  0% {
    background-position: 0 0;
  }
  0% {
    background-position: 500% 0;
  }
}
</style>
