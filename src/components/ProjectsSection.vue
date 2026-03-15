<template>
  <section id="projects" class="section-padding">
    <div class="container" style="max-width: 1200px; margin: 0 auto; padding: 0 24px;">
      <div class="projects-header fade-in">
        <div>
          <h2 class="section-title">Featured <span class="text-gradient">Projects</span></h2>
          <p class="section-subtitle">Latest from my GitHub — you can add screenshots manually.</p>
        </div>
        <a href="https://github.com/Admiral23kizaru?tab=repositories" target="_blank" class="btn-outline-glass all-repos-btn">
          <i class="bi bi-github"></i> All Repos
        </a>
      </div>

      <div v-if="loading" class="loading-grid">
        <div v-for="n in 6" :key="n" class="skeleton-card surface"></div>
      </div>

      <div v-else class="projects-grid">
        <div v-for="(repo, i) in displayedRepos" :key="repo.id" class="project-card surface fade-in" @click="openModal(repo)" :style="{ transitionDelay: (i * 0.08) + 's' }">
          <!-- Image placeholder you can replace -->
          <div class="card-image">
            <img v-if="repo.imageUrl" :src="repo.imageUrl" :alt="repo.name" />
            <div v-else class="card-image-placeholder">
              <i class="bi bi-image" style="font-size: 2rem; color: var(--text-muted);"></i>
              <span style="font-size: 0.75rem; color: var(--text-muted); margin-top: 8px;">Add screenshot</span>
            </div>
          </div>
          <div class="card-body">
            <div class="card-meta">
              <span class="language-dot" :style="{ background: getLanguageColor(repo.language) }"></span>
              <span class="language-name">{{ repo.language || 'Code' }}</span>
              <span class="card-stars" v-if="repo.stargazers_count > 0">
                <i class="bi bi-star-fill"></i> {{ repo.stargazers_count }}
              </span>
            </div>
            <h5 class="card-title">{{ repo.name }}</h5>
            <p class="card-desc">{{ repo.description || 'No description yet.' }}</p>
            <div class="card-footer">
              <span class="card-date"><i class="bi bi-calendar3"></i> {{ formatDate(repo.updated_at) }}</span>
              <span class="card-expand"><i class="bi bi-arrows-angle-expand"></i></span>
            </div>
          </div>
        </div>
      </div>

      <div v-if="!loading && repos.length > 6" class="load-more-wrapper fade-in">
        <button @click="showAll = !showAll" class="btn-outline-glass">
          {{ showAll ? 'Show Less' : `Show All (${repos.length})` }}
        </button>
      </div>
    </div>

    <!-- Modal -->
    <Teleport to="body">
      <Transition name="modal">
        <div v-if="selectedRepo" class="modal-backdrop" @click.self="selectedRepo = null">
          <div class="modal-content surface">
            <div class="modal-header">
              <h4 class="text-gradient">{{ selectedRepo.name }}</h4>
              <button @click="selectedRepo = null" class="modal-close">
                <i class="bi bi-x-lg"></i>
              </button>
            </div>
            <div class="modal-body-content">
              <div class="modal-info">
                <p class="modal-desc">{{ selectedRepo.description || 'No description available.' }}</p>
                <div class="modal-actions">
                  <a :href="selectedRepo.html_url" target="_blank" class="btn-outline-glass">
                    <i class="bi bi-code-slash"></i> View Source
                  </a>
                  <a v-if="selectedRepo.homepage" :href="selectedRepo.homepage" target="_blank" class="btn-electric">
                    <i class="bi bi-box-arrow-up-right"></i> Live Demo
                  </a>
                </div>
              </div>
              <div class="modal-details">
                <div class="surface detail-card">
                  <h6>Tech Stack</h6>
                  <div class="detail-tags">
                    <span v-if="selectedRepo.language" class="tag">{{ selectedRepo.language }}</span>
                  </div>
                </div>
                <div class="surface detail-card">
                  <h6>Git Info</h6>
                  <ul class="git-info-list">
                    <li>⭐ Stars: {{ selectedRepo.stargazers_count }}</li>
                    <li>🍴 Forks: {{ selectedRepo.forks_count }}</li>
                    <li>📅 Updated: {{ formatDate(selectedRepo.updated_at) }}</li>
                    <li>📏 Size: {{ (selectedRepo.size / 1024).toFixed(1) }} MB</li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        </div>
      </Transition>
    </Teleport>
  </section>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

const repos = ref([])
const loading = ref(true)
const selectedRepo = ref(null)
const showAll = ref(false)

const displayedRepos = computed(() => {
  const sorted = [...repos.value]
  if (showAll.value) return sorted
  return sorted.slice(0, 6)
})

const langColors = {
  PHP: '#4F5D95',
  JavaScript: '#F7DF1E',
  TypeScript: '#3178C6',
  Python: '#3776AB',
  HTML: '#E34F26',
  CSS: '#1572B6',
  Vue: '#4FC08D',
  'C#': '#239120',
  Java: '#007396',
  Kotlin: '#A97BFF',
}

function getLanguageColor(lang) {
  return langColors[lang] || '#8b8ba3'
}

function formatDate(dateStr) {
  return new Date(dateStr).toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' })
}

function openModal(repo) {
  selectedRepo.value = repo
}

onMounted(async () => {
  try {
    const res = await fetch('https://api.github.com/users/Admiral23kizaru/repos?per_page=100&sort=updated')
    if (!res.ok) throw new Error('API Error')
    const data = await res.json()
    // Filter out profile config and forks, prioritize personal projects
    repos.value = data.filter(r => !r.fork && r.name !== 'Admiral23kizaru')
  } catch (e) {
    console.error('Failed to fetch repos:', e)
  } finally {
    loading.value = false
  }
})
</script>

<style scoped>
.projects-header {
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  margin-bottom: 40px;
  gap: 16px;
  flex-wrap: wrap;
}

.all-repos-btn {
  padding: 10px 20px;
  font-size: 0.9rem;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  white-space: nowrap;
}

/* Grid */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 24px;
}

.project-card {
  cursor: pointer;
  overflow: hidden;
  border-radius: var(--radius-md);
  transition: transform var(--transition-base), box-shadow var(--transition-base);
}
.project-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 12px 40px rgba(79, 158, 255, 0.15);
}

.card-image {
  height: 180px;
  background: linear-gradient(135deg, rgba(79,158,255,0.06), rgba(139,92,246,0.04));
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}
.card-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.card-image-placeholder {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.card-body {
  padding: 20px;
}

.card-meta {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 10px;
  font-size: 0.82rem;
  color: var(--text-muted);
}

.language-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  flex-shrink: 0;
}

.language-name {
  font-weight: 500;
}

.card-stars {
  margin-left: auto;
  color: #f59e0b;
  font-size: 0.8rem;
}
.card-stars i {
  font-size: 0.7rem;
}

.card-title {
  font-weight: 700;
  font-size: 1.1rem;
  margin-bottom: 8px;
  color: var(--text-primary);
}

.card-desc {
  font-size: 0.88rem;
  color: var(--text-secondary);
  line-height: 1.5;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  margin: 0;
}

.card-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 16px;
  font-size: 0.8rem;
  color: var(--text-muted);
}

.card-expand {
  color: var(--accent-blue);
  transition: transform var(--transition-fast);
}
.project-card:hover .card-expand {
  transform: scale(1.15);
}

/* Skeleton */
.loading-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 24px;
}
.skeleton-card {
  height: 300px;
  animation: pulse 1.5s ease-in-out infinite;
}
@keyframes pulse {
  0%, 100% { opacity: 0.4; }
  50% { opacity: 0.8; }
}

.load-more-wrapper {
  text-align: center;
  margin-top: 32px;
}

/* Modal */
.modal-backdrop {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.7);
  backdrop-filter: blur(8px);
  z-index: 2000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 24px;
}

.modal-content {
  max-width: 700px;
  width: 100%;
  max-height: 85vh;
  overflow-y: auto;
  padding: 0;
  border-radius: var(--radius-lg);
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 24px 28px;
  border-bottom: 1px solid var(--glass-border);
}
.modal-header h4 {
  font-weight: 800;
  font-size: 1.3rem;
  margin: 0;
}

.modal-close {
  background: none;
  border: none;
  color: var(--text-secondary);
  cursor: pointer;
  font-size: 1.2rem;
  padding: 4px;
  transition: color var(--transition-fast);
}
.modal-close:hover {
  color: var(--text-primary);
}

.modal-body-content {
  padding: 28px;
  display: grid;
  grid-template-columns: 1.3fr 1fr;
  gap: 24px;
}

.modal-desc {
  color: var(--text-secondary);
  line-height: 1.7;
  margin-bottom: 24px;
}

.modal-actions {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
}
.modal-actions a {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-size: 0.9rem;
  padding: 10px 20px;
}

.detail-card {
  padding: 16px;
  margin-bottom: 12px;
}
.detail-card h6 {
  font-weight: 700;
  margin-bottom: 10px;
  font-size: 0.9rem;
  color: var(--text-primary);
}

.detail-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.tag {
  background: var(--gradient-glow);
  color: var(--accent-blue);
  padding: 4px 12px;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 500;
}

.git-info-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 6px;
  font-size: 0.85rem;
  color: var(--text-secondary);
}

/* Transitions */
.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.3s ease;
}
.modal-enter-active .modal-content,
.modal-leave-active .modal-content {
  transition: transform 0.3s ease;
}
.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}
.modal-enter-from .modal-content {
  transform: scale(0.95) translateY(20px);
}
.modal-leave-to .modal-content {
  transform: scale(0.95) translateY(20px);
}

@media (max-width: 768px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
  .modal-body-content {
    grid-template-columns: 1fr;
  }
}
</style>
