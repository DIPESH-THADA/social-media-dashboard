<script setup lang="ts">
import { ref, onMounted } from 'vue'

const props = defineProps<{
  label: string
  value: number
  suffix?: string
  change: number
  icon: string
  color: string
  delay?: number
}>()

const displayed = ref(0)

onMounted(() => {
  const start = Date.now()
  const duration = 1200
  const target = props.value
  const delayMs = (props.delay ?? 0) * 50

  setTimeout(() => {
    const tick = () => {
      const elapsed = Date.now() - start
      const progress = Math.min(elapsed / duration, 1)
      const ease = 1 - Math.pow(1 - progress, 3)
      displayed.value = Math.round(ease * target)
      if (progress < 1) requestAnimationFrame(tick)
    }
    requestAnimationFrame(tick)
  }, delayMs)
})

function formatNum(n: number) {
  if (n >= 1_000_000) return (n / 1_000_000).toFixed(1) + 'M'
  if (n >= 1_000) return (n / 1_000).toFixed(1) + 'K'
  return n.toLocaleString()
}
</script>

<template>
  <div class="stat-card fade-up" :class="`fade-up-${delay ?? 1}`">
    <div class="card-top">
      <div class="icon-wrap" :style="{ background: color + '22', color }">
        {{ icon }}
      </div>
      <div class="change" :class="change >= 0 ? 'up' : 'down'">
        {{ change >= 0 ? '▲' : '▼' }} {{ Math.abs(change) }}%
      </div>
    </div>
    <div class="stat-value">{{ formatNum(displayed) }}<span v-if="suffix" class="suffix">{{ suffix }}</span></div>
    <div class="stat-label">{{ label }}</div>
    <div class="bar-track">
      <div class="bar-fill" :style="{ background: color, width: Math.min((value / 10000000) * 100 + 30, 90) + '%' }"></div>
    </div>
  </div>
</template>

<style scoped>
.stat-card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 8px;
  cursor: default;
  transition: border-color 0.25s, transform 0.25s;
  position: relative;
  overflow: hidden;
}
.stat-card::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, transparent 60%, rgba(255,255,255,0.015));
  pointer-events: none;
}
.stat-card:hover {
  border-color: rgba(255,255,255,0.18);
  transform: translateY(-2px);
}
.card-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.icon-wrap {
  width: 40px;
  height: 40px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 18px;
}
.change {
  font-size: 12px;
  font-weight: 500;
  padding: 3px 8px;
  border-radius: 20px;
}
.change.up { color: var(--accent-4); background: rgba(67,233,123,0.1); }
.change.down { color: var(--accent-2); background: rgba(255,111,156,0.1); }
.stat-value {
  font-size: 28px;
  font-weight: 600;
  color: var(--text-h);
  letter-spacing: -0.5px;
  animation: count-up 0.5s ease both;
}
.suffix { font-size: 16px; color: var(--text); margin-left: 2px; }
.stat-label { font-size: 13px; color: var(--text-muted); }
.bar-track {
  height: 3px;
  background: rgba(255,255,255,0.06);
  border-radius: 99px;
  margin-top: 8px;
  overflow: hidden;
}
.bar-fill {
  height: 100%;
  border-radius: 99px;
  opacity: 0.7;
  animation: shimmer 2s ease both;
  transition: width 1.2s cubic-bezier(0.16,1,0.3,1);
}
</style>
