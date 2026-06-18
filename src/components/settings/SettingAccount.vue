<script setup lang="ts">
import { ref } from "vue";

const userInfo = ref({
  firstName: "Dipesh",
  lastName: "Kumar",
  email: "dipesh@example.com",
  phone: "+1 234 567 8900",
  bio: "Social media enthusiast and digital marketer",
  website: "https://example.com",
});

const isEditing = ref(false);
const editForm = ref({ ...userInfo.value });

function startEdit() {
  editForm.value = { ...userInfo.value };
  isEditing.value = true;
}

function saveChanges() {
  userInfo.value = { ...editForm.value };
  isEditing.value = false;
  alert("Profile updated successfully!");
}

function cancelEdit() {
  isEditing.value = false;
}
</script>

<template>
  <div class="account-settings">
    <h2>Account Settings</h2>

    <div class="setting-card">
      <h3>Profile Information</h3>

      <div v-if="!isEditing" class="profile-view">
        <div class="profile-field">
          <label>Name</label>
          <p>{{ userInfo.firstName }} {{ userInfo.lastName }}</p>
        </div>
        <div class="profile-field">
          <label>Email</label>
          <p>{{ userInfo.email }}</p>
        </div>
        <div class="profile-field">
          <label>Phone</label>
          <p>{{ userInfo.phone }}</p>
        </div>
        <div class="profile-field">
          <label>Website</label>
          <p>{{ userInfo.website }}</p>
        </div>
        <div class="profile-field">
          <label>Bio</label>
          <p>{{ userInfo.bio }}</p>
        </div>
        <button class="btn-primary" @click="startEdit">Edit Profile</button>
      </div>

      <div v-else class="profile-form">
        <div class="form-group">
          <label>First Name</label>
          <input v-model="editForm.firstName" type="text" class="input-field" />
        </div>
        <div class="form-group">
          <label>Last Name</label>
          <input v-model="editForm.lastName" type="text" class="input-field" />
        </div>
        <div class="form-group">
          <label>Email</label>
          <input v-model="editForm.email" type="email" class="input-field" />
        </div>
        <div class="form-group">
          <label>Phone</label>
          <input v-model="editForm.phone" type="tel" class="input-field" />
        </div>
        <div class="form-group">
          <label>Website</label>
          <input v-model="editForm.website" type="url" class="input-field" />
        </div>
        <div class="form-group">
          <label>Bio</label>
          <textarea v-model="editForm.bio" class="input-field" rows="4" />
        </div>
        <div class="form-actions">
          <button class="btn-secondary" @click="cancelEdit">Cancel</button>
          <button class="btn-primary" @click="saveChanges">Save Changes</button>
        </div>
      </div>
    </div>

    <div class="setting-card danger">
      <h3>Danger Zone</h3>
      <p class="description">Irreversible actions</p>
      <button class="btn-danger">Delete Account</button>
    </div>
  </div>
</template>

<style scoped>
.account-settings {
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
  margin: 0 0 16px 0;
}

.setting-card.danger {
  border-color: rgba(255, 107, 107, 0.2);
}

.description {
  font-size: 13px;
  color: var(--text-muted);
  margin: 0 0 16px 0;
}

.profile-view,
.profile-form {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.profile-field {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.profile-field label {
  font-size: 12px;
  text-transform: uppercase;
  color: var(--text-muted);
  font-weight: 600;
}

.profile-field p {
  font-size: 14px;
  color: var(--text-h);
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.form-group label {
  font-size: 13px;
  font-weight: 500;
  color: var(--text-h);
}

.input-field {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 10px 12px;
  color: var(--text-h);
  font-size: 14px;
  font-family: var(--sans);
}

.input-field:focus {
  outline: none;
  border-color: var(--accent);
}

.form-actions {
  display: flex;
  gap: 12px;
  margin-top: 16px;
}

.btn-primary,
.btn-secondary,
.btn-danger {
  padding: 10px 16px;
  border-radius: 8px;
  font-size: 14px;
  cursor: pointer;
  border: none;
  font-weight: 500;
  transition: all 0.2s;
}

.btn-primary {
  background: var(--accent);
  color: #fff;
  flex: 1;
}

.btn-primary:hover {
  opacity: 0.88;
}

.btn-secondary {
  background: var(--bg);
  color: var(--text);
  border: 1px solid var(--border);
  flex: 1;
}

.btn-secondary:hover {
  background: var(--bg-hover);
}

.btn-danger {
  background: rgba(255, 107, 107, 0.1);
  color: #ff6b6b;
  border: 1px solid rgba(255, 107, 107, 0.3);
}

.btn-danger:hover {
  background: rgba(255, 107, 107, 0.2);
}
</style>
