<script setup lang="ts">
withDefaults(
  defineProps<{
    label: string
    value: string | number
    trend: string
    direction: 'up' | 'down'
    icon: string
  }>(),
  {
    direction: 'up',
  },
)
</script>

<template>
  <v-card class="metric-card" elevation="0">
    <div class="metric-card-top">
      <div class="metric-label">{{ label }}</div>
      <div class="metric-icon">
        <v-icon :icon="icon" size="18" />
      </div>
    </div>
    <div class="metric-value">{{ value }}</div>
    <div class="metric-trend" :class="direction">
      <span>{{ direction === 'up' ? '▲' : '▼' }} {{ trend }}</span>
      <span class="metric-trend-label">vs last month</span>
    </div>
  </v-card>
</template>
