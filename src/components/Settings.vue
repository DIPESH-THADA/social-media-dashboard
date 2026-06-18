<script setup lang="ts">
import SettingAccount from "./settings/SettingAccount.vue";
import SettingNotifications from "./settings/SettingNotifications.vue";
import SettingPrivacy from "./settings/SettingPrivacy.vue";
import SettingIntegrations from "./settings/SettingIntegrations.vue";
import SettingBilling from "./settings/SettingBilling.vue";

import { ref } from "vue";

const emit = defineEmits<{ (e: "back"): void }>();

const activeTab = ref("account");

const tabs = [
  { id: "account", label: "Account", icon: "👤" },
  { id: "notifications", label: "Notifications", icon: "🔔" },
  { id: "privacy", label: "Privacy", icon: "🔒" },
  { id: "integrations", label: "Integrations", icon: "🔗" },
  { id: "billing", label: "Billing", icon: "💳" },
];
</script>

<template>
  <div class="settings-container">
    <div class="settings-header">
      <button class="back-btn" @click="emit('back')" aria-label="Go back">
        ← Back
      </button>
      <h1>Settings</h1>
    </div>

    <div class="settings-layout">
      <aside class="settings-sidebar">
        <div
          v-for="tab in tabs"
          :key="tab.id"
          class="tab-item"
          :class="{ active: activeTab === tab.id }"
          @click="activeTab = tab.id"
        >
          <span class="tab-icon">{{ tab.icon }}</span>
          <span class="tab-label">{{ tab.label }}</span>
        </div>
      </aside>

      <main class="settings-content">
        <SettingAccount v-if="activeTab === 'account'" />
        <SettingNotifications v-if="activeTab === 'notifications'" />
        <SettingPrivacy v-if="activeTab === 'privacy'" />
        <SettingIntegrations v-if="activeTab === 'integrations'" />
        <SettingBilling v-if="activeTab === 'billing'" />
      </main>
    </div>
  </div>
</template>

<style scoped>
.settings-container {
  min-height: 100svh;
  background: var(--bg);
}

.settings-header {
  padding: 24px;
  border-bottom: 1px solid var(--border);
  display: flex;
  align-items: center;
  gap: 16px;
}

.back-btn {
  background: var(--bg-card);
  border: 1px solid var(--border);
  color: var(--text);
  padding: 8px 12px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 14px;
  transition: all 0.2s;
}

.back-btn:hover {
  background: var(--bg-hover);
  color: var(--text-h);
}

.settings-header h1 {
  font-size: 24px;
  margin: 0;
}

.settings-layout {
  display: grid;
  grid-template-columns: 280px 1fr;
  max-width: 1200px;
  margin: 0 auto;
}

.settings-sidebar {
  border-right: 1px solid var(--border);
  padding: 24px 0;
  height: calc(100svh - 73px);
  overflow-y: auto;
  background: rgba(13, 15, 23, 0.5);
}

.tab-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 24px;
  cursor: pointer;
  color: var(--text);
  transition: all 0.2s;
  border-left: 3px solid transparent;
}

.tab-item:hover {
  background: var(--bg-hover);
  color: var(--text-h);
}

.tab-item.active {
  background: var(--glow-purple);
  color: var(--accent);
  border-left-color: var(--accent);
}

.tab-icon {
  font-size: 18px;
}

.tab-label {
  font-size: 14px;
  font-weight: 500;
}

.settings-content {
  padding: 40px;
  overflow-y: auto;
  height: calc(100svh - 73px);
}

@media (max-width: 900px) {
  .settings-layout {
    grid-template-columns: 1fr;
  }

  .settings-sidebar {
    display: flex;
    gap: 8px;
    border-right: none;
    border-bottom: 1px solid var(--border);
    height: auto;
    overflow-x: auto;
    padding: 0;
    background: transparent;
  }

  .tab-item {
    padding: 12px 16px;
    white-space: nowrap;
    border-left: none;
    border-bottom: 3px solid transparent;
  }

  .tab-item.active {
    border-left: none;
    border-bottom-color: var(--accent);
  }

  .settings-content {
    padding: 24px;
    height: auto;
  }
}

@media (max-width: 600px) {
  .settings-header {
    flex-direction: column;
    align-items: flex-start;
  }

  .settings-content {
    padding: 16px;
  }
}
</style>
