<script setup lang="ts">
import { ref } from 'vue'

const activities = ref([
  { id: 1, platform: '𝕏', platformColor: '#1d9bf0', user: '@dipesh_dev', action: 'retweeted your post about Vue 3', time: '2m ago', avatar: 'D' },
  { id: 2, platform: 'in', platformColor: '#0077b5', user: 'Priya Sharma', action: 'liked your article on TypeScript', time: '14m ago', avatar: 'P' },
  { id: 3, platform: '▶', platformColor: '#ff0000', user: 'CodeWithMe', action: 'commented on your tutorial video', time: '1h ago', avatar: 'C' },
  { id: 4, platform: 'f', platformColor: '#1877f2', user: 'React Community', action: 'shared your post in the group', time: '2h ago', avatar: 'R' },
  { id: 5, platform: '📷', platformColor: '#e1306c', user: 'design.studio', action: 'tagged you in a story', time: '3h ago', avatar: 'S' },
  { id: 6, platform: '𝕏', platformColor: '#1d9bf0', user: '@vue_daily', action: 'followed your account', time: '5h ago', avatar: 'V' },
])
</script>

<template>
  <div class="feed-card fade-up fade-up-4">
    <div class="feed-header">
      <h3>Live activity</h3>
      <span class="live-badge"><span class="live-dot"></span>Live</span>
    </div>
    <ul class="feed-list">
      <li
        v-for="(item, i) in activities"
        :key="item.id"
        class="feed-item"
        :style="{ animationDelay: (i * 0.07) + 's' }"
      >
        <div class="feed-avatar" :style="{ background: item.platformColor + '33', color: item.platformColor }">
          {{ item.avatar }}
        </div>
        <div class="feed-body">
          <div class="feed-meta">
            <strong>{{ item.user }}</strong>
            <span class="platform-tag" :style="{ background: item.platformColor + '22', color: item.platformColor }">
              {{ item.platform }}
            </span>
          </div>
          <p class="feed-action">{{ item.action }}</p>
        </div>
        <div class="feed-time">{{ item.time }}</div>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.feed-card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 20px;
  height: 100%;
}
.feed-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 16px;
}
.feed-header h3 { font-size: 15px; }
.live-badge {
  display: flex;
  align-items: center;
  gap: 5px;
  font-size: 11px;
  color: var(--accent-4);
  background: rgba(67,233,123,0.1);
  padding: 3px 10px;
  border-radius: 99px;
}
.live-dot {
  width: 6px;
  height: 6px;
  background: var(--accent-4);
  border-radius: 50%;
  animation: pulse-ring 1.5s infinite;
}
.feed-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 2px;
}
.feed-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 10px;
  border-radius: 10px;
  cursor: default;
  transition: background 0.2s;
  animation: fadeUp 0.4s ease both;
}
.feed-item:hover { background: var(--bg-hover); }
.feed-avatar {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 600;
  font-size: 13px;
  flex-shrink: 0;
}
.feed-body { flex: 1; min-width: 0; }
.feed-meta {
  display: flex;
  align-items: center;
  gap: 6px;
  margin-bottom: 2px;
}
.feed-meta strong { font-size: 13px; color: var(--text-h); font-weight: 500; }
.platform-tag {
  font-size: 10px;
  padding: 1px 6px;
  border-radius: 4px;
  font-weight: 600;
}
.feed-action {
  font-size: 12px;
  color: var(--text-muted);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.feed-time {
  font-size: 11px;
  color: var(--text-muted);
  flex-shrink: 0;
}
</style>
