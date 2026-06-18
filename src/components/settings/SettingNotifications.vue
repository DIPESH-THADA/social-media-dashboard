<script setup lang="ts">
import { ref } from "vue";

const notifications = ref({
  emailNotifications: true,
  pushNotifications: true,
  postEngagement: true,
  newFollowers: true,
  weeklyDigest: false,
  monthlyReport: true,
  comments: true,
  shares: true,
});

function saveNotifications() {
  alert("Notification settings saved!");
}
</script>

<template>
  <div class="notification-settings">
    <h2>Notification Settings</h2>

    <div class="setting-card">
      <h3>Notification Channels</h3>
      <div class="toggle-group">
        <label class="toggle-item">
          <div class="toggle-header">
            <span class="toggle-label">Email Notifications</span>
            <input
              type="checkbox"
              v-model="notifications.emailNotifications"
              class="toggle-checkbox"
            />
            <span class="toggle-switch"></span>
          </div>
          <p class="toggle-description">Receive important updates via email</p>
        </label>

        <label class="toggle-item">
          <div class="toggle-header">
            <span class="toggle-label">Push Notifications</span>
            <input
              type="checkbox"
              v-model="notifications.pushNotifications"
              class="toggle-checkbox"
            />
            <span class="toggle-switch"></span>
          </div>
          <p class="toggle-description">Get real-time alerts on your device</p>
        </label>
      </div>
    </div>

    <div class="setting-card">
      <h3>Activity Alerts</h3>
      <div class="toggle-group">
        <label class="toggle-item">
          <div class="toggle-header">
            <span class="toggle-label">Post Engagement</span>
            <input
              type="checkbox"
              v-model="notifications.postEngagement"
              class="toggle-checkbox"
            />
            <span class="toggle-switch"></span>
          </div>
          <p class="toggle-description">Notify on likes, comments, and views</p>
        </label>

        <label class="toggle-item">
          <div class="toggle-header">
            <span class="toggle-label">New Followers</span>
            <input
              type="checkbox"
              v-model="notifications.newFollowers"
              class="toggle-checkbox"
            />
            <span class="toggle-switch"></span>
          </div>
          <p class="toggle-description">
            Get alerts when you gain new followers
          </p>
        </label>

        <label class="toggle-item">
          <div class="toggle-header">
            <span class="toggle-label">Comments</span>
            <input
              type="checkbox"
              v-model="notifications.comments"
              class="toggle-checkbox"
            />
            <span class="toggle-switch"></span>
          </div>
          <p class="toggle-description">Notify on new comments on your posts</p>
        </label>

        <label class="toggle-item">
          <div class="toggle-header">
            <span class="toggle-label">Shares</span>
            <input
              type="checkbox"
              v-model="notifications.shares"
              class="toggle-checkbox"
            />
            <span class="toggle-switch"></span>
          </div>
          <p class="toggle-description">Get notified when posts are shared</p>
        </label>
      </div>
    </div>

    <div class="setting-card">
      <h3>Reports</h3>
      <div class="toggle-group">
        <label class="toggle-item">
          <div class="toggle-header">
            <span class="toggle-label">Weekly Digest</span>
            <input
              type="checkbox"
              v-model="notifications.weeklyDigest"
              class="toggle-checkbox"
            />
            <span class="toggle-switch"></span>
          </div>
          <p class="toggle-description">
            Receive weekly summary of your activity
          </p>
        </label>

        <label class="toggle-item">
          <div class="toggle-header">
            <span class="toggle-label">Monthly Report</span>
            <input
              type="checkbox"
              v-model="notifications.monthlyReport"
              class="toggle-checkbox"
            />
            <span class="toggle-switch"></span>
          </div>
          <p class="toggle-description">
            Get detailed monthly performance report
          </p>
        </label>
      </div>
    </div>

    <button class="btn-primary" @click="saveNotifications">
      Save Preferences
    </button>
  </div>
</template>

<style scoped>
.notification-settings {
  display: flex;
  flex-direction: column;
  gap: 24px;
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
  margin: 0 0 20px 0;
}

.toggle-group {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.toggle-item {
  display: flex;
  flex-direction: column;
  gap: 8px;
  cursor: pointer;
  padding: 12px;
  border-radius: 8px;
  transition: background 0.2s;
}

.toggle-item:hover {
  background: var(--bg-hover);
}

.toggle-header {
  display: flex;
  align-items: center;
  gap: 12px;
}

.toggle-label {
  flex: 1;
  font-size: 14px;
  font-weight: 500;
  color: var(--text-h);
}

.toggle-checkbox {
  display: none;
}

.toggle-switch {
  position: relative;
  width: 44px;
  height: 24px;
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 12px;
  transition: all 0.2s;
  flex-shrink: 0;
  display: block;
}

.toggle-checkbox:checked + .toggle-switch {
  background: var(--accent);
  border-color: var(--accent);
}

.toggle-switch::after {
  content: "";
  position: absolute;
  width: 18px;
  height: 18px;
  background: white;
  border-radius: 10px;
  top: 2px;
  left: 2px;
  transition: left 0.2s;
}

.toggle-checkbox:checked + .toggle-switch::after {
  left: 22px;
}

.toggle-description {
  font-size: 12px;
  color: var(--text-muted);
  margin: 0;
  margin-left: 56px;
}

.btn-primary {
  align-self: flex-start;
  background: var(--accent);
  color: #fff;
  border: none;
  padding: 10px 24px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 14px;
  font-weight: 500;
  transition: opacity 0.2s;
}

.btn-primary:hover {
  opacity: 0.88;
}
</style>
