<script setup lang="ts">
import { ref, onMounted } from 'vue'

const platforms = [
  { name: 'Instagram', icon: '📷', color: '#e1306c', followers: 84200, growth: 3.2, posts: 142, reach: '2.1M' },
  { name: 'X (Twitter)', icon: '𝕏', color: '#1d9bf0', followers: 51300, growth: 1.8, posts: 893, reach: '890K' },
  { name: 'LinkedIn', icon: 'in', color: '#0077b5', followers: 28700, growth: 5.6, posts: 67, reach: '440K' },
  { name: 'YouTube', icon: '▶', color: '#ff0000', followers: 19500, growth: 8.1, posts: 24, reach: '1.4M' },
]

const maxFollowers = Math.max(...platforms.map(p => p.followers))
const animated = ref(false)
onMounted(() => { setTimeout(() => { animated.value = true }, 100) })

function ringDash(val: number) {
  const pct = animated.value ? val / maxFollowers : 0
  const circ = 2 * Math.PI * 30
  return `${circ * pct} ${circ}`
}
</script>

<template>
  <div class="platforms-wrap">
    <h3 class="section-title fade-up fade-up-4">Platforms at a glance</h3>
    <div class="platforms-grid">
      <div
        v-for="(p, i) in platforms"
        :key="p.name"
        class="platform-card fade-up"
        :class="`fade-up-${i + 4}`"
      >
        <div class="ring-wrap">
          <svg width="72" height="72" viewBox="0 0 72 72">
            <circle cx="36" cy="36" r="30" fill="none" stroke="rgba(255,255,255,0.05)" stroke-width="6" />
            <circle
              cx="36" cy="36" r="30"
              fill="none"
              :stroke="p.color"
              stroke-width="6"
              stroke-linecap="round"
              :stroke-dasharray="ringDash(p.followers)"
              stroke-dashoffset="0"
              transform="rotate(-90 36 36)"
              style="transition: stroke-dasharray 1s cubic-bezier(0.16,1,0.3,1)"
            />
          </svg>
          <div class="ring-icon" :style="{ color: p.color }">{{ p.icon }}</div>
        </div>
        <div class="platform-info">
          <div class="platform-name">{{ p.name }}</div>
          <div class="platform-followers">{{ (p.followers / 1000).toFixed(1) }}K followers</div>
          <div class="platform-stats">
            <span class="stat-chip">{{ p.posts }} posts</span>
            <span class="stat-chip">{{ p.reach }} reach</span>
          </div>
        </div>
        <div class="platform-growth" :style="{ color: p.color }">+{{ p.growth }}%</div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.section-title {
  font-size: 15px;
  margin-bottom: 14px;
}
.platforms-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
}
.platform-card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 14px;
  padding: 16px;
  display: flex;
  align-items: center;
  gap: 14px;
  cursor: default;
  transition: border-color 0.25s, transform 0.25s;
}
.platform-card:hover {
  border-color: rgba(255,255,255,0.18);
  transform: translateY(-2px);
}
.ring-wrap {
  position: relative;
  width: 72px;
  height: 72px;
  flex-shrink: 0;
}
.ring-icon {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  font-weight: 700;
}
.platform-info { flex: 1; min-width: 0; }
.platform-name { font-size: 13px; font-weight: 500; color: var(--text-h); }
.platform-followers { font-size: 12px; color: var(--text-muted); margin-top: 2px; }
.platform-stats { display: flex; gap: 6px; margin-top: 8px; flex-wrap: wrap; }
.stat-chip {
  font-size: 11px;
  background: rgba(255,255,255,0.05);
  border-radius: 4px;
  padding: 2px 7px;
  color: var(--text-muted);
}
.platform-growth {
  font-size: 13px;
  font-weight: 600;
  flex-shrink: 0;
}
@media (max-width: 600px) {
  .platforms-grid { grid-template-columns: 1fr; }
}
</style>
