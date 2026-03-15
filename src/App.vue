<template>
  <div id="portfolio-app">
    <canvas id="three-bg" ref="threeBg"></canvas>
    <div id="scroll-progress" :style="{ width: scrollProgress + '%' }"></div>
    <NavBar @navigate="scrollTo" />
    <HeroSection />
    <AboutSection />
    <SkillsSection />
    <ProjectsSection />
    <GitHubSection />
    <ContactSection />
    <FooterSection />
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import * as THREE from 'three'
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import GitHubSection from './components/GitHubSection.vue'
import ContactSection from './components/ContactSection.vue'
import FooterSection from './components/FooterSection.vue'

const threeBg = ref(null)
const scrollProgress = ref(0)
let animationId = null

function scrollTo(id) {
  const el = document.getElementById(id)
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}

function handleScroll() {
  const docHeight = document.documentElement.scrollHeight - window.innerHeight
  scrollProgress.value = docHeight > 0 ? (window.scrollY / docHeight) * 100 : 0

  // Intersection observer-based fade-in
  document.querySelectorAll('.fade-in, .fade-in-left, .fade-in-right, .scale-in').forEach(el => {
    const rect = el.getBoundingClientRect()
    if (rect.top < window.innerHeight * 0.88) {
      el.classList.add('visible')
    }
  })
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })
  handleScroll()
  initThree()
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  if (animationId) cancelAnimationFrame(animationId)
})

function initThree() {
  const canvas = threeBg.value
  if (!canvas) return

  const scene = new THREE.Scene()
  const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
  camera.position.z = 5

  const renderer = new THREE.WebGLRenderer({ canvas, alpha: true, antialias: true })
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
  renderer.setSize(window.innerWidth, window.innerHeight)

  // Particle system
  const particleCount = window.innerWidth < 768 ? 800 : 2000
  const geometry = new THREE.BufferGeometry()
  const positions = new Float32Array(particleCount * 3)
  const colors = new Float32Array(particleCount * 3)

  const colorPalette = [
    new THREE.Color('#4f9eff'),
    new THREE.Color('#8b5cf6'),
    new THREE.Color('#22d3ee'),
    new THREE.Color('#ec4899'),
  ]

  for (let i = 0; i < particleCount; i++) {
    positions[i * 3] = (Math.random() - 0.5) * 16
    positions[i * 3 + 1] = (Math.random() - 0.5) * 16
    positions[i * 3 + 2] = (Math.random() - 0.5) * 12

    const c = colorPalette[Math.floor(Math.random() * colorPalette.length)]
    colors[i * 3] = c.r
    colors[i * 3 + 1] = c.g
    colors[i * 3 + 2] = c.b
  }

  geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3))
  geometry.setAttribute('color', new THREE.BufferAttribute(colors, 3))

  const material = new THREE.PointsMaterial({
    size: 0.02,
    vertexColors: true,
    transparent: true,
    opacity: 0.6,
    blending: THREE.AdditiveBlending,
    depthWrite: false,
  })

  const particles = new THREE.Points(geometry, material)
  scene.add(particles)

  // Floating torus wireframe
  const torusGeo = new THREE.TorusGeometry(2.2, 0.08, 16, 100)
  const torusMat = new THREE.MeshBasicMaterial({ color: 0x4f9eff, wireframe: true, transparent: true, opacity: 0.06 })
  const torus = new THREE.Mesh(torusGeo, torusMat)
  scene.add(torus)

  // Second torus
  const torus2Geo = new THREE.TorusGeometry(3, 0.06, 16, 100)
  const torus2Mat = new THREE.MeshBasicMaterial({ color: 0x8b5cf6, wireframe: true, transparent: true, opacity: 0.04 })
  const torus2 = new THREE.Mesh(torus2Geo, torus2Mat)
  torus2.rotation.x = Math.PI / 3
  scene.add(torus2)

  let mouseX = 0, mouseY = 0
  window.addEventListener('mousemove', (e) => {
    mouseX = (e.clientX / window.innerWidth - 0.5) * 2
    mouseY = (e.clientY / window.innerHeight - 0.5) * 2
  })

  window.addEventListener('resize', () => {
    camera.aspect = window.innerWidth / window.innerHeight
    camera.updateProjectionMatrix()
    renderer.setSize(window.innerWidth, window.innerHeight)
  })

  const clock = new THREE.Clock()

  function animate() {
    animationId = requestAnimationFrame(animate)
    const t = clock.getElapsedTime()

    particles.rotation.y = t * 0.03
    particles.rotation.x = t * 0.015

    torus.rotation.x = t * 0.15
    torus.rotation.y = t * 0.1

    torus2.rotation.y = -t * 0.08
    torus2.rotation.z = t * 0.12

    // Subtle mouse parallax
    camera.position.x += (mouseX * 0.3 - camera.position.x) * 0.02
    camera.position.y += (-mouseY * 0.3 - camera.position.y) * 0.02
    camera.lookAt(scene.position)

    renderer.render(scene, camera)
  }

  animate()
}
</script>

<style>
#portfolio-app {
  position: relative;
  z-index: 1;
}
</style>
