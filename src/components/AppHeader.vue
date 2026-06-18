<script setup lang="ts">
import { ref } from "vue";

const emit = defineEmits<{
  (e: "toggle-theme"): void;
  (e: "settings"): void;
}>();

const props = defineProps<{ isDark: boolean }>();
const menuOpen = ref(false);

function navigateToSettings() {
  emit("settings");
  menuOpen.value = false;
}
</script>

<template>
  <header class="header">
    <div class="header-inner">
      <div class="logo">
        <span class="logo-icon">⚡</span>
        <span class="logo-text">SocialPulse</span>
      </div>

      <nav class="nav" :class="{ open: menuOpen }">
        <a href="#" class="nav-link active">Overview</a>
        <a href="#" class="nav-link">Analytics</a>
        <a href="#" class="nav-link">Audience</a>
        <a href="#" class="nav-link">Posts</a>
        <button class="nav-link settings-link" @click="navigateToSettings">Settings</button>
      </nav>

      <div class="header-actions">
        <button
          class="theme-btn"
          @click="$emit('toggle-theme')"
          :aria-label="isDark ? 'Switch to light mode' : 'Switch to dark mode'"
        >
          <span v-if="isDark">☀️</span>
          <span v-else>🌙</span>
        </button>
        <div class="avatar-wrap">
          <div class="avatar">D</div>
          <span class="online-dot"></span>
        </div>
        <button
          class="hamburger"
          @click="menuOpen = !menuOpen"
          aria-label="Toggle menu"
        >
          <span></span><span></span><span></span>
        </button>
      </div>
    </div>
  </header>
</template>

<style scoped>
.header {
  position: sticky;
  top: 0;
  z-index: 100;
  background: rgba(13, 15, 23, 0.85);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--border);
}
.header-inner {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 24px;
  height: 64px;
  display: flex;
  align-items: center;
  gap: 32px;
}
.logo {
  display: flex;
  align-items: center;
  gap: 8px;
  flex-shrink: 0;
}
.logo-icon {
  font-size: 22px;
  filter: drop-shadow(0 0 8px var(--accent));
  animation: float 3s ease-in-out infinite;
}
.logo-text {
  font-size: 17px;
  font-weight: 600;
  color: var(--text-h);
  letter-spacing: -0.3px;
}
.nav {
  display: flex;
  gap: 4px;
  flex: 1;
}
.nav-link {
  padding: 6px 14px;
  border-radius: 8px;
  color: var(--text);
  text-decoration: none;
  font-size: 14px;
  transition:
    color 0.2s,
    background 0.2s;
}
.nav-link:hover {
  color: var(--text-h);
  background: var(--bg-hover);
}
.nav-link.active {
  color: var(--accent);
  background: var(--glow-purple);
}
.settings-link {
  background: none;
  border: none;
  cursor: pointer;
  font-family: var(--sans);
  padding: 6px 14px;
  color: var(--text);
}
.header-actions {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-left: auto;
}
.theme-btn {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 8px;
  width: 36px;
  height: 36px;
  cursor: pointer;
  font-size: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: border-color 0.2s;
}
.theme-btn:hover {
  border-color: var(--accent);
}
.avatar-wrap {
  position: relative;
}
.avatar {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--accent), var(--accent-2));
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 600;
  font-size: 14px;
  color: #fff;
  cursor: pointer;
}
.online-dot {
  position: absolute;
  bottom: 1px;
  right: 1px;
  width: 9px;
  height: 9px;
  background: var(--accent-4);
  border-radius: 50%;
  border: 2px solid var(--bg);
  animation: pulse-ring 2s infinite;
}
.hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px;
}
.hamburger span {
  display: block;
  width: 22px;
  height: 2px;
  background: var(--text);
  border-radius: 2px;
  transition: 0.3s;
}
@media (max-width: 768px) {
  .hamburger {
    display: flex;
  }
  .nav {
    display: none;
    position: absolute;
    top: 64px;
    left: 0;
    right: 0;
    background: var(--bg-card);
    border-bottom: 1px solid var(--border);
    flex-direction: column;
    padding: 12px;
    gap: 4px;
  }
  .nav.open {
    display: flex;
  }
}
</style>
