<template>
  <section id="skills" class="section-padding">
    <div class="container" style="max-width: 1200px; margin: 0 auto; padding: 0 24px;">
      <div class="text-center fade-in" style="margin-bottom: 48px;">
        <h2 class="section-title">Languages, Frameworks & <span class="text-gradient">Tools</span></h2>
        <p class="section-subtitle" style="margin: 0 auto;">A comprehensive and pragmatic stack for all development needs.</p>
      </div>

      <!-- Skills Carousel -->
      <div class="skills-carousel-wrapper fade-in">
        <Carousel :items-to-show="itemsToShow" :wrap-around="true" :autoplay="3000" :transition="500" :pause-autoplay-on-hover="true">
          <Slide v-for="(category, idx) in categories" :key="idx">
            <div class="skill-category-card surface">
              <div class="category-header">
                <span class="category-emoji">{{ category.emoji }}</span>
                <h4 class="category-name">{{ category.name }}</h4>
              </div>
              <div class="skills-grid">
                <div v-for="skill in category.skills" :key="skill.name" class="skill-chip" :style="{ '--chip-color': skill.color }">
                  <img :src="skill.badge" :alt="skill.name" class="skill-badge" loading="lazy" />
                </div>
              </div>
            </div>
          </Slide>

          <template #addons>
            <Navigation />
            <Pagination />
          </template>
        </Carousel>
      </div>

      <!-- Skill Proficiency Chart (simplified with CSS) -->
      <div class="proficiency-section fade-in">
        <h4 class="text-gradient proficiency-title">Skill Proficiency</h4>
        <div class="proficiency-bars">
          <div v-for="bar in proficiencyBars" :key="bar.label" class="bar-item">
            <div class="bar-label">
              <span>{{ bar.label }}</span>
              <span class="bar-value">{{ bar.value }}%</span>
            </div>
            <div class="bar-track">
              <div class="bar-fill" :style="{ width: bar.value + '%', background: bar.gradient }"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel'
import 'vue3-carousel/dist/carousel.css'

const itemsToShow = ref(3)

function updateItemsToShow() {
  if (window.innerWidth < 576) itemsToShow.value = 1
  else if (window.innerWidth < 992) itemsToShow.value = 2
  else itemsToShow.value = 3
}

onMounted(() => {
  updateItemsToShow()
  window.addEventListener('resize', updateItemsToShow)
})
onUnmounted(() => window.removeEventListener('resize', updateItemsToShow))

const badge = (name, color, logo, logoColor = 'white') =>
  `https://img.shields.io/badge/${encodeURIComponent(name)}-${color}?style=for-the-badge&logo=${logo}&logoColor=${logoColor}`

const categories = [
  {
    emoji: '🌐',
    name: 'Frontend & Mobile',
    skills: [
      { name: 'HTML5', color: '#E34F26', badge: badge('HTML5', 'E34F26', 'html5') },
      { name: 'CSS3', color: '#1572B6', badge: badge('CSS3', '1572B6', 'css3') },
      { name: 'JavaScript', color: '#F7DF1E', badge: badge('JavaScript', 'F7DF1E', 'javascript', 'black') },
      { name: 'TypeScript', color: '#3178C6', badge: badge('TypeScript', '3178C6', 'typescript') },
      { name: 'Vue.js', color: '#4FC08D', badge: badge('Vue.js', '4FC08D', 'vuedotjs') },
      { name: 'React', color: '#20232A', badge: badge('React', '20232A', 'react', '61DAFB') },
      { name: 'React Native', color: '#20232A', badge: badge('React Native', '20232A', 'react', '61DAFB') },
      { name: 'Next.js', color: '#000000', badge: badge('Next.js', '000000', 'nextdotjs') },
      { name: 'TailwindCSS', color: '#38B2AC', badge: badge('TailwindCSS', '38B2AC', 'tailwindcss') },
      { name: 'Redux', color: '#764ABC', badge: badge('Redux', '764ABC', 'redux') },
    ],
  },
  {
    emoji: '⚙️',
    name: 'Backend & Database',
    skills: [
      { name: 'Node.js', color: '#339933', badge: badge('Node.js', '339933', 'node.js') },
      { name: 'Express.js', color: '#000000', badge: badge('Express.js', '000000', 'express') },
      { name: 'PHP', color: '#777BB4', badge: badge('PHP', '777BB4', 'php') },
      { name: 'Laravel', color: '#FF2D20', badge: badge('Laravel', 'FF2D20', 'laravel') },
      { name: 'MySQL', color: '#4479A1', badge: badge('MySQL', '4479A1', 'mysql') },
      { name: 'MongoDB', color: '#47A248', badge: badge('MongoDB', '47A248', 'mongodb') },
      { name: 'PostgreSQL', color: '#336791', badge: badge('PostgreSQL', '336791', 'postgresql') },
      { name: 'Firebase', color: '#FFCA28', badge: badge('Firebase', 'FFCA28', 'firebase', 'black') },
    ],
  },
  {
    emoji: '🎮',
    name: 'Game Dev & AI',
    skills: [
      { name: 'Unity', color: '#100000', badge: badge('Unity', '100000', 'unity') },
      { name: 'C#', color: '#239120', badge: badge('C Sharp', '239120', 'csharp') },
      { name: 'Python', color: '#3776AB', badge: badge('Python', '3776AB', 'python') },
      { name: 'n8n', color: '#EA4B71', badge: badge('n8n', 'EA4B71', 'n8n') },
      { name: 'TensorFlow', color: '#FF6F00', badge: badge('TensorFlow', 'FF6F00', 'tensorflow') },
    ],
  },
  {
    emoji: '🚀',
    name: 'Tools & Cloud',
    skills: [
      { name: 'Git', color: '#F05032', badge: badge('Git', 'F05032', 'git') },
      { name: 'Docker', color: '#2496ED', badge: badge('Docker', '2496ED', 'docker') },
      { name: 'AWS', color: '#FF9900', badge: badge('AWS', 'FF9900', 'amazonaws') },
      { name: 'Heroku', color: '#430098', badge: badge('Heroku', '430098', 'heroku') },
    ],
  },
  {
    emoji: '🎨',
    name: 'Design & Security',
    skills: [
      { name: 'Figma', color: '#F24E1E', badge: badge('Figma', 'F24E1E', 'figma') },
      { name: 'Prototyping', color: '#A259FF', badge: badge('Prototyping', 'A259FF', 'figma') },
      { name: 'Pentesting', color: '#2ECC71', badge: badge('Pentester', '2ECC71', 'kalilinux') },
      { name: 'Three.js', color: '#000000', badge: badge('Three.js', '000000', 'threedotjs') },
    ],
  },
]

const proficiencyBars = [
  { label: 'Frontend', value: 92, gradient: 'linear-gradient(90deg, #4f9eff, #22d3ee)' },
  { label: 'Backend', value: 85, gradient: 'linear-gradient(90deg, #8b5cf6, #ec4899)' },
  { label: 'Mobile', value: 88, gradient: 'linear-gradient(90deg, #10b981, #22d3ee)' },
  { label: 'AI / Automation', value: 95, gradient: 'linear-gradient(90deg, #ec4899, #f97316)' },
  { label: 'DevOps', value: 75, gradient: 'linear-gradient(90deg, #4f9eff, #8b5cf6)' },
  { label: 'Game Dev', value: 70, gradient: 'linear-gradient(90deg, #22d3ee, #10b981)' },
  { label: 'UI/UX Design', value: 80, gradient: 'linear-gradient(90deg, #f24e1e, #a259ff)' },
  { label: 'Pentesting', value: 65, gradient: 'linear-gradient(90deg, #2ecc71, #4f9eff)' },
]
</script>

<style scoped>
.skills-carousel-wrapper {
  margin-bottom: 48px;
}

.skill-category-card {
  padding: 28px 24px;
  margin: 8px;
  min-height: 250px;
  display: flex;
  flex-direction: column;
  cursor: grab;
}

.category-header {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 20px;
}

.category-emoji {
  font-size: 1.5rem;
}

.category-name {
  font-weight: 700;
  font-size: 1.05rem;
  color: var(--text-primary);
  margin: 0;
}

.skills-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.skill-chip {
  transition: transform var(--transition-fast);
}
.skill-chip:hover {
  transform: translateY(-3px);
}

.skill-badge {
  height: 28px;
  border-radius: 4px;
}

/* Proficiency */
.proficiency-section {
  max-width: 700px;
  margin: 0 auto;
}

.proficiency-title {
  font-size: 1.3rem;
  font-weight: 700;
  text-align: center;
  margin-bottom: 28px;
}

.proficiency-bars {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.bar-item {
  width: 100%;
}

.bar-label {
  display: flex;
  justify-content: space-between;
  margin-bottom: 6px;
  font-size: 0.88rem;
  font-weight: 500;
}

.bar-value {
  color: var(--text-muted);
  font-family: var(--font-mono);
  font-size: 0.82rem;
}

.bar-track {
  width: 100%;
  height: 6px;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 3px;
  overflow: hidden;
}

.bar-fill {
  height: 100%;
  border-radius: 3px;
  transition: width 1.5s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 0 12px rgba(79, 158, 255, 0.3);
}

.text-center {
  text-align: center;
}
</style>
