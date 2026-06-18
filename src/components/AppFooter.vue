<template>
  <footer class="footer">
    <div class="footer-inner">
      <div class="footer-brand">
        <span class="logo-icon">⚡</span>
        <span class="logo-text">SocialPulse</span>
        <span class="footer-tagline">— All your social data, one place</span>
      </div>
      <div class="footer-links">
        <a href="#">Privacy</a>
        <a href="#">Terms</a>
        <a href="#">Help</a>
        <a href="#">API</a>
      </div>
      <div class="footer-copy">© 2025 SocialPulse. Built with Vue 3 + Vite.</div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  border-top: 1px solid var(--border);
  margin-top: 48px;
}
.footer-inner {
  max-width: 1280px;
  margin: 0 auto;
  padding: 24px 24px;
  display: flex;
  align-items: center;
  gap: 24px;
  flex-wrap: wrap;
}
.footer-brand {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 14px;
}
.logo-icon { font-size: 16px; }
.logo-text { font-weight: 600; color: var(--text-h); }
.footer-tagline { color: var(--text-muted); font-size: 13px; }
.footer-links {
  display: flex;
  gap: 16px;
  margin-left: auto;
}
.footer-links a {
  color: var(--text-muted);
  text-decoration: none;
  font-size: 13px;
  transition: color 0.2s;
}
.footer-links a:hover { color: var(--text-h); }
.footer-copy {
  font-size: 12px;
  color: var(--text-muted);
}
@media (max-width: 640px) {
  .footer-inner { flex-direction: column; align-items: flex-start; gap: 12px; }
  .footer-links { margin-left: 0; }
}
</style>
