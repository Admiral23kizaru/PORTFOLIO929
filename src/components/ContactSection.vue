<template>
  <section id="contact" class="section-padding">
    <div class="container" style="max-width: 1200px; margin: 0 auto; padding: 0 24px;">
      <h2 class="section-title text-center fade-in" style="margin-bottom: 40px;">
        Let's <span class="text-gradient">Connect</span>
      </h2>

      <div class="contact-grid">
        <div class="surface contact-card fade-in-left">
          <div class="contact-card-icon">
            <i class="bi bi-chat-heart"></i>
          </div>
          <h5>Let's Chat</h5>
          <p>Feel free to reach out for collaborations or just a friendly hello.</p>
          <div class="contact-links">
            <a href="https://linkedin.com/in/" target="_blank" class="btn-outline-glass contact-btn">
              <i class="bi bi-linkedin"></i> LinkedIn
            </a>
            <a href="https://twitter.com/" target="_blank" class="btn-outline-glass contact-btn">
              <i class="bi bi-twitter-x"></i> Twitter
            </a>
            <a href="https://github.com/Admiral23kizaru" target="_blank" class="btn-outline-glass contact-btn">
              <i class="bi bi-github"></i> GitHub
            </a>
          </div>
        </div>

        <div class="surface contact-card fade-in-right">
          <div class="contact-card-icon email-icon">
            <i class="bi bi-envelope-heart"></i>
          </div>
          <h5>Email Me</h5>
          <p>Drop me a line for project inquiries or opportunities.</p>
          <a href="mailto:zzephyr934@gmail.com" class="btn-electric email-btn">
            <i class="bi bi-send"></i> zzephyr934@gmail.com
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
  max-width: 800px;
  margin: 0 auto;
}

.contact-card {
  padding: 36px 28px;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.contact-card h5 {
  font-weight: 700;
  font-size: 1.15rem;
  margin-bottom: 8px;
  color: var(--text-primary);
}

.contact-card p {
  color: var(--text-secondary);
  font-size: 0.92rem;
  margin-bottom: 24px;
  line-height: 1.6;
}

.contact-card-icon {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  background: var(--gradient-glow);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  color: var(--accent-blue);
  margin-bottom: 16px;
}

.email-icon {
  color: var(--accent-pink);
}

.contact-links {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
  justify-content: center;
}

.contact-btn {
  padding: 10px 18px;
  font-size: 0.88rem;
  display: inline-flex;
  align-items: center;
  gap: 6px;
}

.email-btn {
  padding: 14px 28px;
  font-size: 0.95rem;
  display: inline-flex;
  align-items: center;
  gap: 8px;
}

.text-center {
  text-align: center;
}

@media (max-width: 768px) {
  .contact-grid {
    grid-template-columns: 1fr;
  }
}
</style>
