<script setup lang="ts">
import { ref } from "vue";

const integrations = ref({
  slack: { connected: true, lastSync: "2 hours ago" },
  zapier: { connected: false, lastSync: null },
  mailchimp: { connected: true, lastSync: "30 minutes ago" },
  buffer: { connected: false, lastSync: null },
});

function toggleIntegration(platform: string) {
  integrations.value[platform as keyof typeof integrations.value].connected =
    !integrations.value[platform as keyof typeof integrations.value].connected;
}
</script>

<template>
  <div class="integrations-settings">
    <h2>Integrations</h2>

    <div class="setting-card">
      <h3>Connected Apps</h3>
      <p class="description">Manage your third-party app connections</p>

      <div class="integration-list">
        <div
          v-for="(data, platform) in integrations"
          :key="platform"
          class="integration-item"
        >
          <div class="integration-header">
            <div class="integration-info">
              <div class="integration-icon">
                <span v-if="platform === 'slack'">🔵</span>
                <span v-else-if="platform === 'zapier'">⚡</span>
                <span v-else-if="platform === 'mailchimp'">📧</span>
                <span v-else-if="platform === 'buffer'">🐦</span>
              </div>
              <div>
                <h4>
                  {{ platform.charAt(0).toUpperCase() + platform.slice(1) }}
                </h4>
                <p v-if="data.connected" class="sync-info">
                  Last synced: {{ data.lastSync }}
                </p>
                <p v-else class="not-connected">Not connected</p>
              </div>
            </div>
            <div
              class="integration-status"
              :class="{ connected: data.connected }"
            >
              {{ data.connected ? "Connected" : "Disconnected" }}
            </div>
          </div>
          <div class="integration-actions">
            <button
              class="btn-action"
              :class="{ disconnect: data.connected }"
              @click="toggleIntegration(platform)"
            >
              {{ data.connected ? "Disconnect" : "Connect" }}
            </button>
          </div>
        </div>
      </div>
    </div>

    <div class="setting-card">
      <h3>Available Integrations</h3>
      <p class="description">Add more apps to your workflow</p>

      <div class="available-integrations">
        <div class="integration-card">
          <div class="integration-icon large">🤖</div>
          <h4>OpenAI</h4>
          <p>AI-powered content generation</p>
          <button class="btn-add">+ Add</button>
        </div>

        <div class="integration-card">
          <div class="integration-icon large">📊</div>
          <h4>Google Analytics</h4>
          <p>Track detailed performance metrics</p>
          <button class="btn-add">+ Add</button>
        </div>

        <div class="integration-card">
          <div class="integration-icon large">💬</div>
          <h4>Discord</h4>
          <p>Get notifications on Discord</p>
          <button class="btn-add">+ Add</button>
        </div>

        <div class="integration-card">
          <div class="integration-icon large">📱</div>
          <h4>Telegram</h4>
          <p>Manage posts via Telegram bot</p>
          <button class="btn-add">+ Add</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.integrations-settings {
  display: flex;
  flex-direction: column;
  gap: 32px;
}

h2 {
  font-size: 24px;
  margin: 0 0 16px 0;
}

.setting-card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 24px;
}

.setting-card h3 {
  font-size: 16px;
  margin: 0 0 12px 0;
}

.description {
  font-size: 13px;
  color: var(--text-muted);
  margin: 0 0 20px 0;
}

.integration-list {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.integration-item {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 16px;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.integration-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}

.integration-info {
  display: flex;
  gap: 12px;
  align-items: flex-start;
}

.integration-icon {
  font-size: 24px;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--glow-purple);
  border-radius: 8px;
}

.integration-info h4 {
  font-size: 14px;
  font-weight: 600;
  margin: 0;
}

.sync-info {
  font-size: 12px;
  color: var(--accent-4);
  margin: 4px 0 0 0;
}

.not-connected {
  font-size: 12px;
  color: var(--text-muted);
  margin: 4px 0 0 0;
}

.integration-status {
  font-size: 12px;
  padding: 6px 12px;
  border-radius: 6px;
  background: rgba(255, 107, 107, 0.1);
  color: #ff6b6b;
  font-weight: 500;
}

.integration-status.connected {
  background: rgba(67, 233, 123, 0.1);
  color: var(--accent-4);
}

.integration-actions {
  display: flex;
  gap: 8px;
}

.btn-action {
  padding: 8px 16px;
  border-radius: 6px;
  border: 1px solid var(--border);
  background: var(--bg-hover);
  color: var(--text);
  font-size: 13px;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-action:hover {
  border-color: var(--accent);
  color: var(--text-h);
}

.btn-action.disconnect {
  background: rgba(255, 107, 107, 0.1);
  border-color: rgba(255, 107, 107, 0.3);
  color: #ff6b6b;
}

.btn-action.disconnect:hover {
  background: rgba(255, 107, 107, 0.2);
}

.available-integrations {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 16px;
}

.integration-card {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 20px;
  text-align: center;
  display: flex;
  flex-direction: column;
  gap: 12px;
  align-items: center;
  transition: all 0.2s;
}

.integration-card:hover {
  border-color: var(--accent);
  background: var(--bg-hover);
}

.integration-icon.large {
  font-size: 32px;
}

.integration-card h4 {
  font-size: 14px;
  margin: 0;
}

.integration-card p {
  font-size: 12px;
  color: var(--text-muted);
  margin: 0;
}

.btn-add {
  background: var(--accent);
  color: #fff;
  border: none;
  padding: 8px 16px;
  border-radius: 6px;
  font-size: 13px;
  cursor: pointer;
  transition: opacity 0.2s;
}

.btn-add:hover {
  opacity: 0.88;
}

@media (max-width: 600px) {
  .available-integrations {
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  }
}
</style>
