<script setup lang="ts">
const posts = [
  { platform: '📷', title: 'Behind the scenes: building with Vue 3', likes: 4821, comments: 312, shares: 1204, reach: '94K', date: 'Jun 14' },
  { platform: '𝕏', title: 'Thread: 10 TypeScript tips that changed how I code', likes: 3209, comments: 497, shares: 2841, reach: '68K', date: 'Jun 12' },
  { platform: '▶', title: 'Full Vite + Vue tutorial for beginners', likes: 2874, comments: 843, shares: 390, reach: '41K', date: 'Jun 9' },
  { platform: 'in', title: 'Why I switched from React to Vue for my startup', likes: 1943, comments: 284, shares: 620, reach: '29K', date: 'Jun 7' },
  { platform: '📷', title: 'My desk setup for remote dev work', likes: 6204, comments: 421, shares: 903, reach: '118K', date: 'Jun 4' },
]

function bar(val: number, max: number) {
  return Math.round((val / max) * 100) + '%'
}
const maxLikes = Math.max(...posts.map(p => p.likes))
</script>

<template>
  <div class="posts-card fade-up fade-up-5">
    <div class="posts-header">
      <h3>Top performing posts</h3>
      <button class="see-all">See all →</button>
    </div>
    <div class="posts-list">
      <div
        v-for="(post, i) in posts"
        :key="i"
        class="post-row"
      >
        <div class="post-rank">{{ i + 1 }}</div>
        <div class="post-platform">{{ post.platform }}</div>
        <div class="post-body">
          <p class="post-title">{{ post.title }}</p>
          <div class="post-bar-track">
            <div class="post-bar" :style="{ width: bar(post.likes, maxLikes) }"></div>
          </div>
        </div>
        <div class="post-metrics">
          <span title="Likes">❤️ {{ post.likes.toLocaleString() }}</span>
          <span title="Reach">👁️ {{ post.reach }}</span>
          <span class="post-date">{{ post.date }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.posts-card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 20px;
}
.posts-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 16px;
}
.posts-header h3 { font-size: 15px; }
.see-all {
  background: none;
  border: none;
  color: var(--accent);
  font-size: 13px;
  cursor: pointer;
  padding: 0;
  font-family: var(--sans);
  transition: opacity 0.2s;
}
.see-all:hover { opacity: 0.7; }
.posts-list { display: flex; flex-direction: column; gap: 4px; }
.post-row {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 10px;
  border-radius: 10px;
  cursor: default;
  transition: background 0.2s;
}
.post-row:hover { background: var(--bg-hover); }
.post-rank {
  font-size: 12px;
  font-weight: 600;
  color: var(--text-muted);
  min-width: 16px;
  text-align: center;
}
.post-platform {
  font-size: 16px;
  width: 24px;
  text-align: center;
  flex-shrink: 0;
}
.post-body { flex: 1; min-width: 0; }
.post-title {
  font-size: 13px;
  color: var(--text-h);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  margin-bottom: 5px;
}
.post-bar-track {
  height: 2px;
  background: rgba(255,255,255,0.05);
  border-radius: 99px;
  overflow: hidden;
}
.post-bar {
  height: 100%;
  background: linear-gradient(90deg, var(--accent), var(--accent-2));
  border-radius: 99px;
  transition: width 1s cubic-bezier(0.16,1,0.3,1);
}
.post-metrics {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 12px;
  color: var(--text-muted);
  flex-shrink: 0;
}
.post-date { color: var(--text-muted); font-size: 11px; }
@media (max-width: 640px) {
  .post-metrics .post-date { display: none; }
}
</style>
