<script setup lang="ts">
import { ref } from "vue";

const privacy = ref({
  profileVisibility: "public",
  allowMessages: true,
  showActivity: true,
  dataCollection: false,
  twoFactorAuth: false,
});

function savePrivacy() {
  alert("Privacy settings saved!");
}
</script>

<template>
  <div class="privacy-settings">
    <h2>Privacy & Security</h2>

    <div class="setting-card">
      <h3>Profile Visibility</h3>
      <div class="radio-group">
        <label class="radio-item">
          <input
            type="radio"
            v-model="privacy.profileVisibility"
            value="public"
          />
          <span class="radio-label">Public</span>
          <p class="radio-description">Anyone can see your profile and posts</p>
        </label>
        <label class="radio-item">
          <input
            type="radio"
            v-model="privacy.profileVisibility"
            value="friends"
          />
          <span class="radio-label">Friends Only</span>
          <p class="radio-description">
            Only your friends can see your profile
          </p>
        </label>
        <label class="radio-item">
          <input
            type="radio"
            v-model="privacy.profileVisibility"
            value="private"
          />
          <span class="radio-label">Private</span>
          <p class="radio-description">Only you can see your profile</p>
        </label>
      </div>
    </div>

    <div class="setting-card">
      <h3>Communication</h3>
      <div class="toggle-group">
        <label class="toggle-item">
          <div class="toggle-header">
            <span class="toggle-label">Allow Messages</span>
            <input
              type="checkbox"
              v-model="privacy.allowMessages"
              class="toggle-checkbox"
            />
            <span class="toggle-switch"></span>
          </div>
          <p class="toggle-description">Let others send you direct messages</p>
        </label>
      </div>
    </div>

    <div class="setting-card">
      <h3>Activity & Data</h3>
      <div class="toggle-group">
        <label class="toggle-item">
          <div class="toggle-header">
            <span class="toggle-label">Show Activity Status</span>
            <input
              type="checkbox"
              v-model="privacy.showActivity"
              class="toggle-checkbox"
            />
            <span class="toggle-switch"></span>
          </div>
          <p class="toggle-description">Let others see when you're online</p>
        </label>

        <label class="toggle-item">
          <div class="toggle-header">
            <span class="toggle-label">Allow Analytics Collection</span>
            <input
              type="checkbox"
              v-model="privacy.dataCollection"
              class="toggle-checkbox"
            />
            <span class="toggle-switch"></span>
          </div>
          <p class="toggle-description">
            Help us improve by collecting usage data
          </p>
        </label>
      </div>
    </div>

    <div class="setting-card">
      <h3>Security</h3>
      <div class="toggle-group">
        <label class="toggle-item">
          <div class="toggle-header">
            <span class="toggle-label">Two-Factor Authentication</span>
            <input
              type="checkbox"
              v-model="privacy.twoFactorAuth"
              class="toggle-checkbox"
            />
            <span class="toggle-switch"></span>
          </div>
          <p class="toggle-description">Add extra security to your account</p>
        </label>
      </div>
      <button class="btn-secondary">Change Password</button>
    </div>

    <button class="btn-primary" @click="savePrivacy">
      Save Security Settings
    </button>
  </div>
</template>

<style scoped>
.privacy-settings {
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
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.setting-card h3 {
  font-size: 16px;
  margin: 0;
}

.radio-group {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.radio-item {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  padding: 12px;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.2s;
}

.radio-item:hover {
  background: var(--bg-hover);
}

.radio-item input[type="radio"] {
  margin-top: 4px;
  cursor: pointer;
  accent-color: var(--accent);
}

.radio-label {
  font-size: 14px;
  font-weight: 500;
  color: var(--text-h);
}

.radio-description {
  font-size: 12px;
  color: var(--text-muted);
  margin: 2px 0 0 0;
}

.toggle-group {
  display: flex;
  flex-direction: column;
  gap: 12px;
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

.btn-primary,
.btn-secondary {
  align-self: flex-start;
  padding: 10px 16px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 14px;
  font-weight: 500;
  border: none;
  transition: all 0.2s;
}

.btn-primary {
  background: var(--accent);
  color: #fff;
}

.btn-primary:hover {
  opacity: 0.88;
}

.btn-secondary {
  background: var(--bg);
  color: var(--text);
  border: 1px solid var(--border);
}

.btn-secondary:hover {
  background: var(--bg-hover);
}
</style>
