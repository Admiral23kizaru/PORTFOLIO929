<template>
  <footer class="portfolio-footer">
    <div class="container" style="max-width: 1200px; margin: 0 auto; padding: 0 24px;">
      <div class="footer-content">
        <span class="footer-logo text-gradient">Aaron</span>
        <p class="footer-text">
          © {{ new Date().getFullYear() }} Aaron — Built with
          <i class="bi bi-heart-fill" style="color: var(--accent-pink);"></i>
          Vue.js & Three.js
        </p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.portfolio-footer {
  padding: 32px 0;
  border-top: 1px solid var(--glass-border);
  background: rgba(6, 6, 11, 0.5);
}

.footer-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.footer-logo {
  font-size: 1.4rem;
  font-weight: 800;
}

.footer-text {
  font-size: 0.85rem;
  color: var(--text-muted);
  margin: 0;
}

@media (max-width: 768px) {
  .footer-content {
    flex-direction: column;
    gap: 12px;
    text-align: center;
  }
}
</style>
