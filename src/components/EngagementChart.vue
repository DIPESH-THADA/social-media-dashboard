<script setup lang="ts">
import { ref, onMounted } from 'vue'

const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
const datasets = [
  { label: 'Instagram', color: '#e1306c', data: [420, 580, 390, 700, 610, 830, 720] },
  { label: 'X (Twitter)', color: '#1d9bf0', data: [310, 420, 280, 530, 490, 600, 550] },
  { label: 'LinkedIn', color: '#0077b5', data: [180, 240, 210, 330, 290, 410, 380] },
]
const maxVal = 900
const animated = ref(false)

onMounted(() => {
  setTimeout(() => { animated.value = true }, 200)
})

function barHeight(val: number) {
  return animated.value ? (val / maxVal) * 160 + 'px' : '0px'
}

const activeDay = ref<number | null>(null)
</script>

<template>
  <div class="chart-card fade-up fade-up-3">
    <div class="chart-header">
      <h3>Weekly engagement</h3>
      <div class="legend">
        <span v-for="d in datasets" :key="d.label" class="legend-item">
          <span class="legend-dot" :style="{ background: d.color }"></span>
          {{ d.label }}
        </span>
      </div>
    </div>

    <div class="chart-body">
      <div class="y-axis">
        <span>900</span><span>600</span><span>300</span><span>0</span>
      </div>
      <div class="bars-area">
        <div
          v-for="(day, di) in days"
          :key="day"
          class="day-group"
          @mouseenter="activeDay = di"
          @mouseleave="activeDay = null"
        >
          <div class="bars">
            <div
              v-for="ds in datasets"
              :key="ds.label"
              class="bar"
              :style="{
                height: barHeight(ds.data[di]),
                background: ds.color,
                opacity: activeDay === null || activeDay === di ? 1 : 0.3,
                transitionDelay: (di * 0.05) + 's'
              }"
            ></div>
          </div>
          <div class="day-label" :class="{ active: activeDay === di }">{{ day }}</div>
          <div v-if="activeDay === di" class="tooltip">
            <div v-for="ds in datasets" :key="ds.label" class="tooltip-row">
              <span class="tt-dot" :style="{ background: ds.color }"></span>
              <span>{{ ds.label }}: <strong>{{ ds.data[di] }}</strong></span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.chart-card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 20px;
}
.chart-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 20px;
  flex-wrap: wrap;
  gap: 8px;
}
.chart-header h3 { font-size: 15px; }
.legend {
  display: flex;
  gap: 14px;
  flex-wrap: wrap;
}
.legend-item {
  display: flex;
  align-items: center;
  gap: 5px;
  font-size: 12px;
  color: var(--text-muted);
}
.legend-dot {
  width: 8px;
  height: 8px;
  border-radius: 2px;
}
.chart-body {
  display: flex;
  gap: 8px;
  align-items: flex-end;
}
.y-axis {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 180px;
  padding-bottom: 24px;
  font-size: 10px;
  color: var(--text-muted);
  text-align: right;
  min-width: 28px;
}
.bars-area {
  display: flex;
  flex: 1;
  gap: 8px;
  align-items: flex-end;
}
.day-group {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 6px;
  position: relative;
  cursor: default;
}
.bars {
  display: flex;
  gap: 3px;
  align-items: flex-end;
  height: 160px;
}
.bar {
  width: 10px;
  border-radius: 4px 4px 0 0;
  transition: height 0.8s cubic-bezier(0.16,1,0.3,1), opacity 0.2s;
  transform-origin: bottom;
}
.day-label {
  font-size: 11px;
  color: var(--text-muted);
  transition: color 0.2s;
}
.day-label.active { color: var(--text-h); }
.tooltip {
  position: absolute;
  bottom: calc(100% + 8px);
  left: 50%;
  transform: translateX(-50%);
  background: #1e2030;
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 8px 12px;
  min-width: 140px;
  z-index: 10;
  animation: fadeUp 0.15s ease;
  box-shadow: 0 8px 24px rgba(0,0,0,0.4);
}
.tooltip-row {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 12px;
  color: var(--text);
  padding: 2px 0;
}
.tt-dot {
  width: 6px;
  height: 6px;
  border-radius: 2px;
  flex-shrink: 0;
}
.tooltip-row strong { color: var(--text-h); }
</style>
