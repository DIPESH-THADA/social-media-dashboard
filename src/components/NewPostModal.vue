<script setup lang="ts">
import { ref } from "vue";

interface Post {
  platform: string;
  content: string;
  scheduledTime?: string;
}

const emit = defineEmits<{
  (e: "close"): void;
  (e: "post-created", post: Post): void;
}>();

const formData = ref({
  content: "",
  platforms: {
    twitter: false,
    instagram: false,
    facebook: false,
    linkedin: false,
  },
  schedule: false,
  scheduledTime: "",
});

const characterCount = ref(0);
const maxCharacters = 280;

function updateCharCount() {
  characterCount.value = formData.value.content.length;
}

function handleSubmit() {
  if (!formData.value.content.trim()) {
    alert("Please enter some content for your post");
    return;
  }

  const selectedPlatforms = Object.entries(formData.value.platforms)
    .filter(([_, selected]) => selected)
    .map(([platform]) => platform);

  if (selectedPlatforms.length === 0) {
    alert("Please select at least one platform");
    return;
  }

  selectedPlatforms.forEach((platform) => {
    emit("post-created", {
      platform,
      content: formData.value.content,
      scheduledTime: formData.value.schedule
        ? formData.value.scheduledTime
        : undefined,
    });
  });

  resetForm();
  emit("close");
}

function resetForm() {
  formData.value = {
    content: "",
    platforms: {
      twitter: false,
      instagram: false,
      facebook: false,
      linkedin: false,
    },
    schedule: false,
    scheduledTime: "",
  };
  characterCount.value = 0;
}
</script>

<template>
  <div class="modal-overlay" @click.self="emit('close')">
    <div class="modal-content fade-up">
      <div class="modal-header">
        <h2>Create New Post</h2>
        <button
          class="close-btn"
          @click="emit('close')"
          aria-label="Close modal"
        >
          ✕
        </button>
      </div>

      <form @submit.prevent="handleSubmit" class="modal-form">
        <div class="form-group">
          <label for="content">Post Content</label>
          <textarea
            id="content"
            v-model="formData.content"
            @input="updateCharCount"
            placeholder="What's on your mind? ✨"
            class="textarea"
            :class="{ warning: characterCount > maxCharacters }"
          />
          <div
            class="char-count"
            :class="{ warning: characterCount > maxCharacters }"
          >
            {{ characterCount }} / {{ maxCharacters }}
          </div>
        </div>

        <div class="form-group">
          <label>Select Platforms</label>
          <div class="platforms-grid">
            <label class="platform-checkbox">
              <input type="checkbox" v-model="formData.platforms.twitter" />
              <span class="platform-label">🐦 Twitter</span>
            </label>
            <label class="platform-checkbox">
              <input type="checkbox" v-model="formData.platforms.instagram" />
              <span class="platform-label">📷 Instagram</span>
            </label>
            <label class="platform-checkbox">
              <input type="checkbox" v-model="formData.platforms.facebook" />
              <span class="platform-label">📘 Facebook</span>
            </label>
            <label class="platform-checkbox">
              <input type="checkbox" v-model="formData.platforms.linkedin" />
              <span class="platform-label">💼 LinkedIn</span>
            </label>
          </div>
        </div>

        <div class="form-group">
          <label class="schedule-label">
            <input type="checkbox" v-model="formData.schedule" />
            <span>Schedule post</span>
          </label>
          <input
            v-if="formData.schedule"
            type="datetime-local"
            v-model="formData.scheduledTime"
            class="input-datetime"
          />
        </div>

        <div class="modal-actions">
          <button type="button" class="btn-secondary" @click="emit('close')">
            Cancel
          </button>
          <button type="submit" class="btn-primary">Post Now</button>
        </div>
      </form>
    </div>
  </div>
</template>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  backdrop-filter: blur(4px);
}

.modal-content {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 32px;
  max-width: 500px;
  width: 90%;
  max-height: 90vh;
  overflow-y: auto;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.4);
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 24px;
}

.modal-header h2 {
  font-size: 22px;
  margin: 0;
}

.close-btn {
  background: none;
  border: none;
  font-size: 24px;
  cursor: pointer;
  color: var(--text-muted);
  transition: color 0.2s;
  padding: 0;
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.close-btn:hover {
  color: var(--text-h);
}

.modal-form {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.form-group label {
  font-size: 14px;
  font-weight: 500;
  color: var(--text-h);
}

.textarea {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 12px 16px;
  color: var(--text-h);
  font-family: var(--sans);
  font-size: 14px;
  resize: vertical;
  min-height: 120px;
  transition: border-color 0.2s;
}

.textarea:focus {
  outline: none;
  border-color: var(--accent);
}

.textarea.warning {
  border-color: #ff6b6b;
  background: rgba(255, 107, 107, 0.05);
}

.char-count {
  font-size: 12px;
  color: var(--text-muted);
  text-align: right;
}

.char-count.warning {
  color: #ff6b6b;
}

.platforms-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 12px;
}

.platform-checkbox {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 12px;
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s;
}

.platform-checkbox:hover {
  background: var(--bg-hover);
  border-color: var(--accent);
}

.platform-checkbox input[type="checkbox"] {
  cursor: pointer;
  width: 16px;
  height: 16px;
}

.platform-checkbox input[type="checkbox"]:checked + .platform-label {
  color: var(--accent);
}

.platform-label {
  font-size: 14px;
  font-weight: 500;
}

.schedule-label {
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
  font-weight: 500;
}

.schedule-label input[type="checkbox"] {
  cursor: pointer;
}

.input-datetime {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 8px 12px;
  color: var(--text-h);
  font-size: 14px;
}

.input-datetime:focus {
  outline: none;
  border-color: var(--accent);
}

.modal-actions {
  display: flex;
  gap: 12px;
  margin-top: 16px;
}

.btn-primary,
.btn-secondary {
  flex: 1;
  padding: 11px 20px;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
  border: none;
  font-family: var(--sans);
}

.btn-primary {
  background: var(--accent);
  color: #fff;
}

.btn-primary:hover {
  opacity: 0.88;
  transform: translateY(-1px);
}

.btn-secondary {
  background: var(--bg);
  color: var(--text);
  border: 1px solid var(--border);
}

.btn-secondary:hover {
  background: var(--bg-hover);
  border-color: var(--accent);
}

@media (max-width: 600px) {
  .modal-content {
    padding: 24px;
  }

  .platforms-grid {
    grid-template-columns: 1fr;
  }
}
</style>
