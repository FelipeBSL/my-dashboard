<script setup lang="ts">
import { computed, ref } from 'vue'

import MetricCard from '@/components/MetricCard.vue'
import metricsData from '@/data/metrics.json'

interface Region {
  name: string
  shipmentVolume: number
  onTimeDeliveryPct: number
  openExceptions: number
  shipmentTrend: number
  onTimeTrend: number
  exceptionsTrend: number
}

interface TrendPoint {
  month: string
  shipments: number
}

const overview = {
  ...metricsData.overview,
  name: 'All Regions',
}
const regions = metricsData.regions as Region[]
const selectedRegion = ref('All Regions')

const regionOptions = ['All Regions', ...regions.map((region) => region.name)]

const selectedMetrics = computed(() => {
  if (selectedRegion.value === 'All Regions') return overview

  return regions.find((region) => region.name === selectedRegion.value) ?? overview
})

const visibleRegions = computed(() => {
  if (selectedRegion.value === 'All Regions') return regions

  return regions.filter((region) => region.name === selectedRegion.value)
})

const trendPoints = computed(
  () =>
    (metricsData.monthlyTrends[selectedRegion.value as keyof typeof metricsData.monthlyTrends] ??
      metricsData.monthlyTrends['All Regions']) as TrendPoint[],
)

const trendMax = computed(() => Math.max(...trendPoints.value.map((point) => point.shipments)))
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
        <div class="section-heading">
          <h2 class="section-title">Key Metrics</h2>
          <v-select
            v-model="selectedRegion"
            class="region-filter"
            label="View region"
            :items="regionOptions"
            variant="outlined"
            density="comfortable"
            hide-details
          />
        </div>
        <v-row class="metrics-grid">
          <v-col cols="12" sm="6" lg="3">
            <MetricCard
              label="Shipment Volume"
              :value="selectedMetrics.shipmentVolume.toLocaleString()"
              :trend="`${selectedMetrics.shipmentTrend}%`"
              direction="up"
              icon="mdi-truck-outline"
            />
          </v-col>
          <v-col cols="12" sm="6" lg="3">
            <MetricCard
              label="On-Time Delivery"
              :value="`${selectedMetrics.onTimeDeliveryPct}%`"
              :trend="`${selectedMetrics.onTimeTrend}%`"
              :direction="selectedMetrics.onTimeTrend >= 0 ? 'up' : 'down'"
              icon="mdi-clock-check-outline"
            />
          </v-col>
          <v-col cols="12" sm="6" lg="3">
            <MetricCard
              label="Open Exceptions"
              :value="selectedMetrics.openExceptions"
              :trend="`${selectedMetrics.exceptionsTrend}`"
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
          <div class="region-row" v-for="region in visibleRegions" :key="region.name">
            <span class="region-name">{{ region.name }}</span>
            <div class="region-bar-track">
              <div class="region-bar-fill" :style="{ width: region.onTimeDeliveryPct + '%' }"></div>
              </div>
              <span class="region-value">{{ region.onTimeDeliveryPct }}%</span>
          </div>
        </div>
            </v-card>
          </v-col>
        </v-row>

        <div class="section-heading trends-heading">
          <h2 class="section-title">Trends</h2>
          <span class="filter-caption">{{ selectedRegion }} · monthly shipment volume</span>
        </div>
        <v-card class="chart-section" elevation="0">
          <div class="trend-chart" role="img" :aria-label="`Monthly shipment volume for ${selectedRegion}`">
            <div v-for="point in trendPoints" :key="point.month" class="trend-column">
              <span class="trend-value">{{ point.shipments.toLocaleString() }}</span>
              <div class="trend-bar-track">
                <div
                  class="trend-bar-fill"
                  :style="{ height: `${(point.shipments / trendMax) * 100}%` }"
                ></div>
              </div>
              <span class="trend-month">{{ point.month }}</span>
            </div>
          </div>
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

.section-heading {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 24px;
}

.region-filter {
  max-width: 220px;
  margin-top: -12px;
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

.trends-heading {
  align-items: baseline;
}

.filter-caption {
  color: var(--text-secondary);
  font-size: 0.8rem;
  font-weight: 200;
}

.trend-chart {
  display: flex;
  align-items: flex-end;
  justify-content: space-around;
  gap: 20px;
  width: 100%;
  min-height: 280px;
  padding: 24px 12px 0;
}

.trend-column {
  display: flex;
  align-items: center;
  flex: 1;
  flex-direction: column;
  gap: 8px;
  height: 240px;
}

.trend-value {
  color: var(--text-secondary);
  font-size: 0.75rem;
  font-weight: 300;
  white-space: nowrap;
}

.trend-bar-track {
  display: flex;
  align-items: flex-end;
  width: min(64px, 100%);
  flex: 1;
  overflow: hidden;
  border-radius: 8px 8px 2px 2px;
  background: rgba(255, 255, 255, 0.08);
}

.trend-bar-fill {
  width: 100%;
  min-height: 10px;
  border-radius: 8px 8px 2px 2px;
  background: linear-gradient(180deg, #22d3ee, #6366f1);
  transition: height 0.3s ease;
}

.trend-month {
  color: var(--text-secondary);
  font-size: 0.8rem;
  font-weight: 300;
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
  .dashboard-bar {
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

  .section-heading {
    align-items: stretch;
    flex-direction: column;
    gap: 8px;
  }

  .region-filter {
    max-width: none;
    margin: 0 0 12px;
  }

  .trends-heading {
    align-items: flex-start;
  }
}
</style>
