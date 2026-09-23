<script setup lang="ts">
import MetricCard from '@/components/MetricCard.vue'

interface Region {
  name: string
  onTimePct: number
}

// Placeholder dataset — will be replaced by src/data/metrics.json in Step 2.4
const metrics = {
  shipmentVolume: 48231,
  onTimeDeliveryPct: 94.7,
  openExceptions: 27,
  regions: [
    { name: 'Northeast', onTimePct: 92 },
    { name: 'Midwest', onTimePct: 88 },
    { name: 'South', onTimePct: 81 },
    { name: 'West', onTimePct: 95 },
  ] as Region[],
}
</script>

<template>
  <v-app>
    <v-app-bar class="dashboard-bar" elevation="0">
      <div class="brand">
        <span class="brand-name">FastForward</span>
        <span class="brand-suffix">Ops Dashboard</span>
      </div>
      <v-spacer />
      <div class="header-meta">
        Executive Overview<br />
        Last updated: Sep 14, 2026
      </div>
    </v-app-bar>

    <v-main>
      <v-container class="dashboard-main">
        <h2 class="section-title">Key Metrics</h2>
        <v-row class="metrics-grid">
          <v-col cols="12" sm="6" lg="3">
            <MetricCard
              label="Shipment Volume"
              :value="metrics.shipmentVolume.toLocaleString()"
              trend="6.2%"
              direction="up"
              icon="mdi-truck-outline"
            />
          </v-col>
          <v-col cols="12" sm="6" lg="3">
            <MetricCard
              label="On-Time Delivery"
              :value="`${metrics.onTimeDeliveryPct}%`"
              trend="1.3%"
              direction="up"
              icon="mdi-clock-check-outline"
            />
          </v-col>
          <v-col cols="12" sm="6" lg="3">
            <MetricCard
              label="Open Exceptions"
              :value="metrics.openExceptions"
              trend="4"
              direction="down"
              icon="mdi-alert-outline"
            />
          </v-col>
          <v-col cols="12" sm="6" lg="6">
            <v-card class="metric-card card-regional" elevation="0">
        <div class="metric-card-top">
          <div class="metric-label">Regional Performance</div>
          <div class="metric-icon">
            <v-icon icon="mdi-map-marker-outline" size="18" />
          </div>
        </div>
        <div class="region-list">
          <div class="region-row" v-for="region in metrics.regions" :key="region.name">
            <span class="region-name">{{ region.name }}</span>
            <div class="region-bar-track">
              <div class="region-bar-fill" :style="{ width: region.onTimePct + '%' }"></div>
            </div>
            <span class="region-value">{{ region.onTimePct }}%</span>
          </div>
        </div>
            </v-card>
          </v-col>
        </v-row>

        <h2 class="section-title">Trends</h2>
        <v-card class="chart-section" elevation="0">
          <div class="chart-placeholder">Chart section — coming soon</div>
        </v-card>
      </v-container>
    </v-main>

    <footer>FastForward Ops Dashboard &mdash; internal build &mdash; v0.1.0-shell</footer>
  </v-app>
</template>

<style scoped>
.dashboard-bar {
  position: relative !important;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 28px 40px;
  background: rgba(255, 255, 255, 0.04);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border-bottom: 1px solid var(--card-border);
}

.brand {
  display: flex;
  align-items: baseline;
  gap: 10px;
}

.brand-name {
  font-weight: 800;
  font-size: 1.5rem;
  letter-spacing: 0.5px;
}

.brand-suffix {
  font-weight: 200;
  font-size: 1.1rem;
  color: var(--text-secondary);
  letter-spacing: 1px;
}

.header-meta {
  font-weight: 200;
  font-size: 0.85rem;
  color: var(--text-secondary);
  text-align: right;
}

.dashboard-main {
  padding: 40px;
  max-width: 1280px;
  margin: 0 auto;
}

.section-title {
  font-weight: 200;
  font-size: 0.8rem;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--text-secondary);
  margin: 0 0 20px 4px;
}

.metrics-grid {
  margin-bottom: 48px;
}

.metric-card {
  background: var(--card-bg);
  border: 1px solid var(--card-border);
  border-radius: 18px;
  padding: 24px;
  backdrop-filter: blur(14px);
  -webkit-backdrop-filter: blur(14px);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.25);
  transition:
    transform 0.25s ease,
    box-shadow 0.25s ease;
  height: 100%;
}

.metric-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.35);
}

.metric-card-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 18px;
}

.metric-icon {
  width: 36px;
  height: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 10px;
  background: rgba(99, 102, 241, 0.15);
  color: var(--accent-glow);
}

.metric-label {
  font-weight: 200;
  font-size: 0.8rem;
  letter-spacing: 1px;
  text-transform: uppercase;
  color: var(--text-secondary);
  margin-bottom: 8px;
}

.metric-value {
  font-weight: 800;
  font-size: 2.2rem;
  line-height: 1.1;
}

.metric-trend {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  margin-top: 12px;
  font-weight: 300;
  font-size: 0.85rem;
}

.metric-trend.up {
  color: var(--accent-up);
}

.metric-trend.down {
  color: var(--accent-down);
}

.metric-trend-label {
  color: var(--text-secondary);
  font-weight: 200;
}

.region-list {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.region-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
}

.region-name {
  font-weight: 300;
  font-size: 0.9rem;
  width: 90px;
  flex-shrink: 0;
}

.region-bar-track {
  flex: 1;
  height: 8px;
  border-radius: 4px;
  background: rgba(255, 255, 255, 0.08);
  overflow: hidden;
}

.region-bar-fill {
  height: 100%;
  border-radius: 4px;
  background: linear-gradient(90deg, #6366f1, #22d3ee);
}

.region-value {
  font-weight: 700;
  font-size: 0.9rem;
  width: 46px;
  text-align: right;
}

.chart-section {
  background: var(--card-bg);
  border: 1px solid var(--card-border);
  border-radius: 18px;
  padding: 24px;
  backdrop-filter: blur(14px);
  -webkit-backdrop-filter: blur(14px);
  min-height: 260px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.chart-placeholder {
  font-weight: 200;
  color: var(--text-secondary);
  font-size: 0.9rem;
  letter-spacing: 0.5px;
}

footer {
  display: block;
  text-align: center;
  padding: 24px 40px 40px;
  font-weight: 200;
  font-size: 0.75rem;
  color: var(--text-secondary);
  letter-spacing: 0.5px;
}

@media (max-width: 640px) {
  header {
    flex-direction: column;
    align-items: flex-start;
    gap: 8px;
  }

  .header-meta {
    text-align: left;
  }

  .dashboard-main {
    padding: 24px;
  }
}
</style>
