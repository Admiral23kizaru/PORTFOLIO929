<template>
  <header id="home" class="hero">
    <div class="container hero-container">
      <div class="hero-content fade-in">
        <p class="hero-tag">👋 Welcome</p>
        <h1 class="hero-title">
          Hello, I'm <span class="text-gradient">Aaron</span>
        </h1>
        <p class="hero-description">
          Web & Mobile App Developer — building modern, scalable products with clean UX
          and strong engineering foundations.
        </p>
        <div class="hero-actions">
          <a href="#projects" class="btn-electric">
            <i class="bi bi-rocket-takeoff"></i> View My Projects
          </a>
          <a href="#contact" class="btn-outline-glass">
            <i class="bi bi-chat-dots"></i> Contact
          </a>
        </div>

        <div class="hero-stats">
          <div class="stat-item">
            <span class="stat-number text-gradient">20+</span>
            <span class="stat-label">Projects</span>
          </div>
          <div class="stat-divider"></div>
          <div class="stat-item">
            <span class="stat-number text-gradient">5+</span>
            <span class="stat-label">Languages</span>
          </div>
          <div class="stat-divider"></div>
          <div class="stat-item">
            <span class="stat-number text-gradient">∞</span>
            <span class="stat-label">Passion</span>
          </div>
        </div>
      </div>

      <div class="hero-portrait scale-in">
        <div class="portrait-wrapper">
          <div class="holo-ring"></div>
          <div class="holo-ring ring-2"></div>
          <img
            src="https://github.com/Admiral23kizaru.png"
            alt="Aaron Portrait"
            class="portrait-img"
          />
        </div>
      </div>
    </div>

    <div class="scroll-indicator fade-in">
      <div class="mouse">
        <div class="wheel"></div>
      </div>
      <span>Scroll Down</span>
    </div>
  </header>
</template>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  position: relative;
  padding: 100px 0 60px;
}

.hero-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 60px;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
}

.hero-content {
  flex: 1;
  max-width: 620px;
}

.hero-tag {
  font-size: 0.95rem;
  font-weight: 600;
  color: var(--text-secondary);
  text-transform: uppercase;
  letter-spacing: 3px;
  margin-bottom: 16px;
}

.hero-title {
  font-size: clamp(2.4rem, 5vw, 3.8rem);
  font-weight: 900;
  line-height: 1.1;
  margin-bottom: 20px;
  letter-spacing: -1px;
}

.hero-description {
  font-size: 1.1rem;
  color: var(--text-secondary);
  line-height: 1.7;
  margin-bottom: 32px;
  max-width: 520px;
}

.hero-actions {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
  margin-bottom: 48px;
}

.hero-actions .btn-electric,
.hero-actions .btn-outline-glass {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: 1rem;
  padding: 14px 32px;
}

.hero-stats {
  display: flex;
  align-items: center;
  gap: 24px;
}

.stat-item {
  text-align: center;
}

.stat-number {
  display: block;
  font-size: 1.8rem;
  font-weight: 800;
}

.stat-label {
  font-size: 0.82rem;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 1px;
}

.stat-divider {
  width: 1px;
  height: 40px;
  background: var(--glass-border);
}

/* Portrait */
.hero-portrait {
  flex-shrink: 0;
}

.portrait-wrapper {
  position: relative;
  width: clamp(240px, 22vw, 340px);
  height: clamp(240px, 22vw, 340px);
}

.portrait-img {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  object-fit: cover;
  position: relative;
  z-index: 2;
  border: 3px solid rgba(79, 158, 255, 0.3);
}

.holo-ring {
  position: absolute;
  inset: -12px;
  border-radius: 50%;
  border: 2px solid transparent;
  border-top-color: var(--accent-blue);
  border-right-color: var(--accent-violet);
  animation: spin 4s linear infinite;
  z-index: 1;
}

.ring-2 {
  inset: -24px;
  border-top-color: var(--accent-pink);
  border-left-color: var(--accent-cyan);
  animation-duration: 6s;
  animation-direction: reverse;
  opacity: 0.5;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

/* Scroll indicator */
.scroll-indicator {
  position: absolute;
  bottom: 32px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  color: var(--text-muted);
  font-size: 0.75rem;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.mouse {
  width: 22px;
  height: 34px;
  border: 2px solid var(--text-muted);
  border-radius: 11px;
  display: flex;
  justify-content: center;
  padding-top: 6px;
}

.wheel {
  width: 3px;
  height: 8px;
  background: var(--accent-blue);
  border-radius: 2px;
  animation: scroll-wheel 1.5s ease-in-out infinite;
}

@keyframes scroll-wheel {
  0% { opacity: 1; transform: translateY(0); }
  100% { opacity: 0; transform: translateY(8px); }
}

@media (max-width: 768px) {
  .hero-container {
    flex-direction: column-reverse;
    text-align: center;
  }
  .hero-content {
    align-items: center;
    display: flex;
    flex-direction: column;
  }
  .hero-description {
    text-align: center;
  }
  .hero-actions {
    justify-content: center;
  }
  .hero-stats {
    justify-content: center;
  }
  .portrait-wrapper {
    width: 200px;
    height: 200px;
  }
  .scroll-indicator {
    display: none;
  }
}
</style>
