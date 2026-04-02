<template>
  <section id="github-stats" class="section-padding">
    <div class="container" style="max-width: 1200px; margin: 0 auto; padding: 0 24px;">
      <h2 class="section-title text-center fade-in" style="margin-bottom: 40px;">
        GitHub <span class="text-gradient">Overview</span>
      </h2>

      <div class="github-grid">
        <!-- Contribution Graph -->
        <div class="surface github-card fade-in-left">
          <h5 class="card-heading"><i class="bi bi-graph-up"></i> Contribution Graph</h5>
          <div class="chart-wrapper">
            <img src="https://ghchart.rshah.org/4f9eff/Admiral23kizaru" alt="Contribution Graph" loading="lazy" />
          </div>
        </div>

        <!-- Terminal Card -->
        <div class="surface github-card fade-in-right">
          <h5 class="card-heading"><i class="bi bi-terminal"></i> System Status</h5>
          <div class="terminal">
            <div class="terminal-dots">
              <span class="dot red"></span>
              <span class="dot yellow"></span>
              <span class="dot green"></span>
            </div>
            <div class="terminal-body">
              <TerminalLine prefix="$" color="var(--accent-blue)">init portfolio_analytics --verbose</TerminalLine>
              <TerminalLine prefix=">" v-for="(line, i) in terminalLines" :key="i" :color="line.color">
                {{ line.text }}
              </TerminalLine>
              <TerminalLine prefix="$" color="var(--accent-blue)" style="margin-top: 8px;">status check</TerminalLine>
              <TerminalLine prefix=">" color="var(--accent-emerald)">ALL SYSTEMS OPERATIONAL</TerminalLine>
              <span class="cursor">_</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Contribution Snake -->
      <div class="surface snake-card fade-in" style="margin-top: 24px;">
        <h5 class="card-heading text-center"><i class="bi bi-activity"></i> Contribution Snake</h5>
        <div class="snake-wrapper">
          <picture>
            <source media="(prefers-color-scheme: dark)"
              srcset="https://raw.githubusercontent.com/Admiral23kizaru/Admiral23kizaru/output/github-contribution-grid-snake-dark.svg" />
            <source media="(prefers-color-scheme: light)"
              srcset="https://raw.githubusercontent.com/Admiral23kizaru/Admiral23kizaru/output/github-contribution-grid-snake.svg" />
            <img
              src="https://raw.githubusercontent.com/Admiral23kizaru/Admiral23kizaru/output/github-contribution-grid-snake.svg"
              alt="Contribution snake" loading="lazy" />
          </picture>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { h } from 'vue'

const TerminalLine = (props, { slots }) => {
  return h('div', { class: 'terminal-line' }, [
    h('span', { style: { color: 'var(--text-muted)' } }, props.prefix + ' '),
    h('span', { style: { color: props.color || 'var(--text-secondary)' } }, slots.default?.()),
  ])
}
TerminalLine.props = ['prefix', 'color']

const terminalLines = [
  { text: 'Loading modules... Done', color: 'var(--accent-emerald)' },
  { text: 'Fetching repos... 25+ Found', color: 'var(--accent-cyan)' },
  { text: 'Analyzing commits... 4,500+ Detected', color: '#f59e0b' },
  { text: 'Calculating scaling... Exponential 🚀', color: 'var(--text-primary)' },
]
</script>

<style scoped>
.github-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
}

.github-card {
  padding: 28px;
}

.card-heading {
  font-weight: 700;
  font-size: 1rem;
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  gap: 8px;
  color: var(--text-primary);
}

.chart-wrapper {
  overflow: hidden;
  border-radius: var(--radius-sm);
}
.chart-wrapper img {
  width: 100%;
  filter: brightness(0.95);
}

/* Terminal */
.terminal {
  background: #0d1117;
  border: 1px solid #30363d;
  border-radius: var(--radius-sm);
  padding: 16px;
  font-family: var(--font-mono);
  font-size: 0.82rem;
  min-height: 200px;
}

.terminal-dots {
  display: flex;
  gap: 6px;
  margin-bottom: 16px;
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}
.dot.red { background: #ff5f56; }
.dot.yellow { background: #ffbd2e; }
.dot.green { background: #27c93f; }

.terminal-line {
  margin-bottom: 3px;
  line-height: 1.6;
}

.cursor {
  color: var(--text-muted);
  animation: blink 1s step-end infinite;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}

/* Snake */
.snake-card {
  padding: 28px;
}

.snake-wrapper {
  overflow: hidden;
  border-radius: var(--radius-sm);
}
.snake-wrapper img {
  width: 100%;
}

.text-center {
  text-align: center;
}

@media (max-width: 768px) {
  .github-grid {
    grid-template-columns: 1fr;
  }
}
</style>
