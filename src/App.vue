<script setup lang="ts">
import { ref } from "vue";
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";
import StatCard from "./components/StatCard.vue";
import ActivityFeed from "./components/ActivityFeed.vue";
import EngagementChart from "./components/EngagementChart.vue";
import PlatformCards from "./components/PlatformCards.vue";
import TopPosts from "./components/TopPosts.vue";
import NewPostModal from "./components/NewPostModal.vue";
import Settings from "./components/Settings.vue";

const isDark = ref(true);
const showNewPostModal = ref(false);
const currentPage = ref("dashboard");
const postedContent =
  ref < Array<{ platform: string; content: string; time: string }>([]);

function toggleTheme() {
  isDark.value = !isDark.value;
  document.documentElement.setAttribute(
    "data-theme",
    isDark.value ? "dark" : "light",
  );
}

function handlePostCreated(post: {
  platform: string;
  content: string;
  scheduledTime?: string;
}) {
  postedContent.value.unshift({
    platform: post.platform,
    content: post.content,
    time: new Date().toLocaleTimeString(),
  });
  alert(`✓ Post created successfully on ${post.platform}!`);
}

function exportReport() {
  const report = {
    generatedAt: new Date().toLocaleString(),
    stats: stats,
    postedContent: postedContent.value,
    totalReach: 4900000,
    averageEngagement: 6800,
  };

  const csvContent = [
    ["SocialPulse Monthly Report", new Date().toLocaleString()],
    [],
    ["Statistics"],
    ["Metric", "Value", "Change"],
    ...stats.map((s) => [s.label, s.value, `${s.change}%`]),
    [],
    ["Posted Content", "Count:", postedContent.value.length],
    ["Platform", "Content", "Time"],
    ...postedContent.value.map((p) => [p.platform, `"${p.content}"`, p.time]),
  ]
    .map((row) => row.join(","))
    .join("\n");

  const blob = new Blob([csvContent], { type: "text/csv" });
  const url = window.URL.createObjectURL(blob);
  const link = document.createElement("a");
  link.href = url;
  link.download = `SocialPulse-Report-${Date.now()}.csv`;
  link.click();
  window.URL.revokeObjectURL(url);
}

const stats = [
  {
    label: "Total followers",
    value: 183700,
    change: 4.2,
    icon: "👥",
    color: "#7c6fff",
  },
  {
    label: "Monthly reach",
    value: 4900000,
    change: 11.3,
    icon: "📡",
    color: "#ff6f9c",
  },
  {
    label: "Avg. engagement",
    value: 6800,
    suffix: "/post",
    change: -1.4,
    icon: "💬",
    color: "#4fc3f7",
  },
  {
    label: "Posts this month",
    value: 48,
    change: 20.0,
    icon: "📝",
    color: "#43e97b",
  },
];
</script>

<template>
  <div :class="['app-root', isDark ? 'dark' : 'light']">
    <AppHeader :isDark="isDark" @toggle-theme="toggleTheme" @settings="currentPage = 'settings'" />

    <Settings v-if="currentPage === 'settings'" @back="currentPage = 'dashboard'" />

    <main v-else class="main">
      <div class="container">
        <!-- Hero greeting -->
        <div class="hero-bar fade-up fade-up-1">
          <div>
            <h1 class="page-title">Good morning, Dipesh 👋</h1>
            <p class="page-sub">
              Here's how your social presence looks today —
              <span class="highlight">June 18, 2026</span>
            </p>
          </div>
          <div class="hero-actions">
            <button class="btn-secondary" @click="exportReport">Export report</button>
            <button class="btn-primary" @click="showNewPostModal = true">+ New post</button>
          </div>
        </div>

        <!-- Stat cards row -->
        <div class="stats-grid">
          <StatCard
            v-for="(s, i) in stats"
            :key="s.label"
            v-bind="s"
            :delay="i + 1"
          />
        </div>

        <!-- Main content grid -->
        <div class="content-grid">
          <div class="col-left">
            <EngagementChart />
            <TopPosts />
          </div>
          <div class="col-right">
            <ActivityFeed />
            <PlatformCards />
          </div>
        </div>
      </div>
    </main>

    <AppFooter />

    <NewPostModal
      v-if="showNewPostModal"
      @close="showNewPostModal = false"
      @post-created="handlePostCreated"
    />
  </div>
</template>

<style>
/* Light theme overrides */
.light {
  --bg: #f5f6fa;
  --bg-card: #ffffff;
  --bg-hover: #f0f1f8;
  --border: rgba(0, 0, 0, 0.08);
  --text: #555770;
  --text-h: #0d0f1c;
  --text-muted: #9298b0;
  --glow-purple: rgba(124, 111, 255, 0.1);
}
.light .header {
  background: rgba(245, 246, 250, 0.9) !important;
}
</style>

<style scoped>
.app-root {
  min-height: 100svh;
  display: flex;
  flex-direction: column;
}
.main {
  flex: 1;
  padding: 32px 0 48px;
}
.container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 24px;
}

.hero-bar {
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  gap: 16px;
  margin-bottom: 28px;
  flex-wrap: wrap;
}
.page-title {
  font-size: 28px;
  letter-spacing: -0.5px;
  margin-bottom: 4px;
}
.page-sub {
  font-size: 14px;
  color: var(--text-muted);
}
.highlight {
  color: var(--accent);
}
.hero-actions {
  display: flex;
  gap: 10px;
  flex-shrink: 0;
}
.btn-primary {
  background: var(--accent);
  color: #fff;
  border: none;
  border-radius: 10px;
  padding: 9px 18px;
  font-size: 14px;
  cursor: pointer;
  font-family: var(--sans);
  transition:
    opacity 0.2s,
    transform 0.15s;
}
.btn-primary:hover {
  opacity: 0.88;
  transform: translateY(-1px);
}
.btn-secondary {
  background: transparent;
  color: var(--text);
  border: 1px solid var(--border);
  border-radius: 10px;
  padding: 9px 18px;
  font-size: 14px;
  cursor: pointer;
  font-family: var(--sans);
  transition:
    border-color 0.2s,
    color 0.2s;
}
.btn-secondary:hover {
  border-color: var(--accent);
  color: var(--text-h);
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 14px;
  margin-bottom: 20px;
}

.content-grid {
  display: grid;
  grid-template-columns: 1fr 380px;
  gap: 20px;
  align-items: start;
}
.col-left,
.col-right {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

@media (max-width: 1100px) {
  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
  }
  .content-grid {
    grid-template-columns: 1fr;
  }
}
@media (max-width: 600px) {
  .stats-grid {
    grid-template-columns: 1fr 1fr;
  }
  .page-title {
    font-size: 22px;
  }
}
@media (max-width: 420px) {
  .stats-grid {
    grid-template-columns: 1fr;
  }
}
</style>
