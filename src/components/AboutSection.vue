<template>
  <section id="about" class="section-padding">
    <div class="container" style="max-width: 1200px; margin: 0 auto; padding: 0 24px;">
      <div class="about-grid">
        <div class="about-text fade-in-left">
          <h2 class="section-title">About <span class="text-gradient">Me</span></h2>
          <p class="section-subtitle" style="margin-bottom: 24px;">
            Passionate about modern, responsive, and user-friendly applications. Specialized in
            mobile dev (React Native, Kotlin) and full‑stack web. Exploring DevOps & Cloud,
            and continuously learning ML/AI.
          </p>
          <div class="surface about-highlights">
            <div class="highlight-item" v-for="item in highlights" :key="item.text">
              <i class="bi bi-check2-circle"></i>
              <span>{{ item.text }}</span>
            </div>
          </div>
        </div>

        <div class="about-cards fade-in-right">
          <div class="surface about-card" v-for="(card, i) in cards" :key="i">
            <div class="icon-bubble">
              <i :class="card.icon"></i>
            </div>
            <div>
              <h5 class="card-title">{{ card.title }}</h5>
              <p class="card-desc">{{ card.desc }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const highlights = [
  { text: 'Mobile & Web development' },
  { text: 'DevOps & Cloud' },
  { text: 'Machine Learning & AI' },
  { text: 'Open‑source contributor' },
  { text: 'Figma Prototyping & UI Design' },
  { text: 'Penetration Testing & Security' },
]

const cards = [
  { icon: 'bi bi-laptop', title: 'Web Applications', desc: 'Modern SPAs and SSR apps with Vue, React — performance‑focused and accessible.' },
  { icon: 'bi bi-phone', title: 'Mobile Apps', desc: 'Cross‑platform apps with React Native and native Android (Kotlin/Java).' },
  { icon: 'bi bi-robot', title: 'AI Automation', desc: 'Expert n8n AI Automation Builder for seamless workflows and intelligent bots.' },
  { icon: 'bi bi-cloud', title: 'DevOps & Cloud', desc: 'CI/CD, Docker, and AWS deployments for reliable, scalable delivery.' },
]
</script>

<style scoped>
.about-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 48px;
  align-items: start;
}

.about-highlights {
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.highlight-item {
  display: flex;
  align-items: center;
  gap: 12px;
  color: var(--text-secondary);
  font-size: 0.95rem;
}
.highlight-item i {
  color: var(--accent-cyan);
  font-size: 1.1rem;
}

.about-cards {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.about-card {
  padding: 20px;
  display: flex;
  gap: 16px;
  align-items: flex-start;
}

.card-title {
  font-weight: 700;
  font-size: 1rem;
  margin-bottom: 4px;
  color: var(--text-primary);
}

.card-desc {
  font-size: 0.88rem;
  color: var(--text-secondary);
  line-height: 1.5;
  margin: 0;
}

@media (max-width: 768px) {
  .about-grid {
    grid-template-columns: 1fr;
    gap: 32px;
  }
}
</style>
