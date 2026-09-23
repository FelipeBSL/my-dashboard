<script setup lang="ts">
import { RouterView } from 'vue-router'
</script>

<template>
  <div class="bg-gradient"></div>
  <div class="bokeh bokeh-1"></div>
  <div class="bokeh bokeh-2"></div>
  <div class="bokeh bokeh-3"></div>

  <RouterView />
</template>

<style scoped>
/* Slow-moving gradient background */
.bg-gradient {
  position: fixed;
  inset: 0;
  z-index: -2;
  background: linear-gradient(120deg, #0b0e17, #141a2e, #1a1030, #0e1a2b);
  background-size: 400% 400%;
  animation: gradientShift 30s ease infinite;
}

@keyframes gradientShift {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

/* Bokeh shapes */
.bokeh {
  position: fixed;
  z-index: -1;
  border-radius: 50%;
  filter: blur(60px);
  opacity: 0.35;
  pointer-events: none;
}

.bokeh-1 {
  width: 420px;
  height: 420px;
  top: -100px;
  left: -80px;
  background: radial-gradient(circle, #6366f1, transparent 70%);
  animation: floatSlow 22s ease-in-out infinite;
}

.bokeh-2 {
  width: 320px;
  height: 320px;
  top: 40%;
  right: -60px;
  background: radial-gradient(circle, #22d3ee, transparent 70%);
  animation: floatSlow 26s ease-in-out infinite reverse;
}

.bokeh-3 {
  width: 280px;
  height: 280px;
  bottom: -80px;
  left: 30%;
  background: radial-gradient(circle, #f472b6, transparent 70%);
  animation: floatSlow 34s ease-in-out infinite;
}

@keyframes floatSlow {
  0%,
  100% {
    transform: translate(0, 0) scale(1);
  }
  50% {
    transform: translate(40px, -30px) scale(1.08);
  }
}
</style>
