<template>
  <nav class="navbar" :class="{ scrolled: isScrolled, 'mobile-open': isMobileOpen }">
    <div class="container nav-container">
      <a href="#home" class="nav-logo" @click.prevent="$emit('navigate', 'home')">
        <span class="logo-text text-gradient">Aaron</span>
      </a>

      <button class="nav-toggle" @click="isMobileOpen = !isMobileOpen" :aria-expanded="isMobileOpen" aria-label="Toggle navigation">
        <span class="toggle-bar" :class="{ open: isMobileOpen }"></span>
      </button>

      <div class="nav-links" :class="{ open: isMobileOpen }">
        <a v-for="link in links" :key="link.id" :href="'#' + link.id" class="nav-link" @click.prevent="navigate(link.id)">
          {{ link.label }}
        </a>
        <a href="https://github.com/Admiral23kizaru" target="_blank" class="btn-electric nav-cta">
          <i class="bi bi-github"></i> GitHub
        </a>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const emit = defineEmits(['navigate'])
const isScrolled = ref(false)
const isMobileOpen = ref(false)

const links = [
  { id: 'about', label: 'About' },
  { id: 'skills', label: 'Skills' },
  { id: 'projects', label: 'Projects' },
  { id: 'github-stats', label: 'GitHub' },
  { id: 'contact', label: 'Contact' },
]

function navigate(id) {
  isMobileOpen.value = false
  emit('navigate', id)
}

function handleScroll() {
  isScrolled.value = window.scrollY > 30
}

onMounted(() => window.addEventListener('scroll', handleScroll, { passive: true }))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  padding: 18px 0;
  transition: var(--transition-base);
}

.navbar.scrolled {
  background: rgba(6, 6, 11, 0.85);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--glass-border);
  padding: 10px 0;
}

.nav-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
}

.nav-logo {
  font-size: 1.6rem;
  font-weight: 800;
  letter-spacing: -0.5px;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 8px;
}

.nav-link {
  padding: 8px 16px;
  font-size: 0.92rem;
  font-weight: 500;
  color: var(--text-secondary);
  border-radius: var(--radius-sm);
  transition: var(--transition-fast);
}
.nav-link:hover {
  color: var(--text-primary);
  background: rgba(255, 255, 255, 0.04);
}

.nav-cta {
  margin-left: 8px;
  padding: 8px 20px;
  font-size: 0.88rem;
  display: inline-flex;
  align-items: center;
  gap: 6px;
}

.nav-toggle {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
  z-index: 1001;
}

.toggle-bar {
  display: block;
  width: 24px;
  height: 2px;
  background: var(--text-primary);
  position: relative;
  transition: var(--transition-fast);
}
.toggle-bar::before,
.toggle-bar::after {
  content: '';
  position: absolute;
  left: 0;
  width: 24px;
  height: 2px;
  background: var(--text-primary);
  transition: var(--transition-fast);
}
.toggle-bar::before { top: -7px; }
.toggle-bar::after { top: 7px; }
.toggle-bar.open { background: transparent; }
.toggle-bar.open::before { top: 0; transform: rotate(45deg); }
.toggle-bar.open::after { top: 0; transform: rotate(-45deg); }

@media (max-width: 768px) {
  .nav-toggle {
    display: block;
  }
  .nav-links {
    position: fixed;
    top: 0;
    right: -100%;
    width: 280px;
    height: 100vh;
    background: rgba(6, 6, 11, 0.97);
    backdrop-filter: blur(20px);
    flex-direction: column;
    align-items: flex-start;
    padding: 80px 32px 32px;
    gap: 4px;
    transition: right var(--transition-base);
    border-left: 1px solid var(--glass-border);
  }
  .nav-links.open {
    right: 0;
  }
  .nav-link {
    font-size: 1.05rem;
    padding: 12px 16px;
    width: 100%;
  }
  .nav-cta {
    margin-left: 0;
    margin-top: 16px;
    width: 100%;
    justify-content: center;
  }
}
</style>
