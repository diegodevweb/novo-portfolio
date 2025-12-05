<template>
  <section :id="id" class="hero-section relative-position overflow-hidden">
    <!-- Background animated grid -->
    <div class="hero-grid-bg"></div>

    <!-- Floating particles -->
    <div class="particles-container">
      <div v-for="i in 20" :key="i" class="particle" :style="getParticleStyle()"></div>
    </div>

    <div class="container q-py-xl">
      <div class="row items-center q-col-gutter-xl">
        <!-- Left side - Content -->
        <div class="col-12 col-md-7" data-aos="fade-right">
          <div class="text-caption text-primary text-uppercase q-mb-sm text-weight-bold letter-spacing">
            <q-icon name="code" size="16px" class="q-mr-xs" />
            Full Stack Developer · Laravel & Vue.js
          </div>

          <h1 class="hero-title text-h2 text-weight-bold q-mb-md">
            Olá, sou <span class="text-primary">Diego Rodrigues</span>
          </h1>

          <div class="hero-subtitle text-h5 text-grey-4 q-mb-sm">
            <span class="typing-text">{{ typingText }}</span>
            <span class="typing-cursor">|</span>
          </div>

          <p class="text-body1 text-grey-4 q-mb-lg q-mt-md" style="max-width: 600px; line-height: 1.8;">
            Desenvolvo <strong class="text-white">sistemas web robustos e escaláveis</strong> há mais de 3 anos.
            Especializado em integrações complexas (NFe, SEFAZ, APIs), automações,
            filas de processamento e dashboards administrativos que <strong class="text-white">agregam valor ao negócio</strong>.
          </p>

          <!-- Stats -->
<!--          <div class="row q-col-gutter-md q-mb-lg">-->
<!--            <div class="col-auto" v-for="stat in stats" :key="stat.label">-->
<!--              <div class="stat-card bg-grey-9 rounded-borders q-pa-md text-center">-->
<!--                <div class="text-h4 text-weight-bold text-primary">{{ stat.value }}</div>-->
<!--                <div class="text-caption text-grey-4">{{ stat.label }}</div>-->
<!--              </div>-->
<!--            </div>-->
<!--          </div>-->

          <!-- CTA Buttons -->
          <div class="row q-gutter-md">
            <q-btn
              outline
              color="grey-4"
              size="lg"
              label="Baixar CV"
              icon="picture_as_pdf"
              :href="cvLink"
              target="_blank"
              class="cta-button-secondary"
            />
            <q-btn
              flat
              round
              color="grey-4"
              icon="mdi-linkedin"
              size="lg"
              :href="linkedinLink"
              target="_blank"
              class="social-button"
            >
              <q-tooltip>LinkedIn</q-tooltip>
            </q-btn>
            <q-btn
              flat
              round
              color="grey-4"
              icon="mdi-github"
              size="lg"
              :href="githubLink"
              target="_blank"
              class="social-button"
            >
              <q-tooltip>GitHub</q-tooltip>
            </q-btn>
          </div>
        </div>

        <!-- Right side - Visual Card -->
        <div class="col-12 col-md-5" data-aos="fade-left" data-aos-delay="200">
          <q-card flat class="hero-card bg-grey-9 rounded-borders overflow-hidden">
            <!-- Gradient border effect -->
            <div class="gradient-border"></div>

            <q-card-section class="q-pa-lg">
              <!-- Avatar / Profile Image -->
              <div class="text-center q-mb-lg">
                <div class="avatar-container">
                  <q-avatar size="120px" class="avatar-main">
                    <img src="src/assets/perfil1.jpg" alt="Diego Rodrigues">
                  </q-avatar>
                  <div class="avatar-ring"></div>
                  <div class="status-badge bg-positive">
                    <q-icon name="circle" size="8px" />
<!--                    <span class="q-ml-xs text-caption">Disponível</span>-->
                  </div>
                </div>
              </div>

              <!-- Main Stack -->
              <div class="q-mb-md">
                <div class="text-subtitle2 text-grey-4 q-mb-sm">
                  Stack Principal
                </div>
                <div class="row q-gutter-xs">
                  <q-chip
                    v-for="tech in mainStack"
                    :key="tech.name"
                    :color="tech.color"
                    text-color="white"
                    size="sm"
                    class="stack-chip"
                  >
                    <q-icon :name="tech.icon" size="16px" class="q-mr-xs" v-if="tech.icon" />
                    {{ tech.name }}
                  </q-chip>
                </div>
              </div>

              <q-separator class="q-my-md" dark />

              <!-- Current Status -->
              <div class="q-mb-md">
                <div class="text-subtitle2 text-grey-4 q-mb-sm">
                  <q-icon name="work" size="18px" class="q-mr-xs" />
                  Atualmente
                </div>
                <p class="text-body2 text-grey-3 q-mb-xs">
                  🏢 <strong>Claro</strong> - Full Stack Developer
                </p>
                <p class="text-body2 text-grey-3">
                  💼 <strong>Tevah Solutions</strong> - Projetos sob demanda
                </p>
              </div>

              <q-separator class="q-my-md" dark />

              <!-- Location & Availability -->
              <div>
                <div class="row items-center justify-between">
                  <div class="text-body2 text-grey-4">
                    <q-icon name="location_on" size="16px" class="q-mr-xs" />
                    Campinas, SP - Brasil
                  </div>
                  <q-badge color="positive" class="q-px-sm">
                    Remoto
                  </q-badge>
                </div>
              </div>
            </q-card-section>

            <!-- Decorative elements -->
            <div class="card-decoration card-decoration-1"></div>
            <div class="card-decoration card-decoration-2"></div>
          </q-card>

          <!-- Floating badges -->
          <div class="floating-badges">
            <q-badge
              color="primary"
              class="floating-badge badge-1"
              style="padding: 8px 12px;"
            >
              <q-icon name="check_circle" size="16px" class="q-mr-xs" />
              3+ anos
            </q-badge>
            <q-badge
              color="positive"
              class="floating-badge badge-2"
              style="padding: 8px 12px;"
            >
              <q-icon name="code" size="16px" class="q-mr-xs" />
              Laravel Expert
            </q-badge>
          </div>
        </div>
      </div>
    </div>

    <!-- Scroll indicator -->
    <div class="scroll-indicator" @click="$emit('scrollTo', 'about')">
      <q-icon name="keyboard_arrow_down" size="32px" class="scroll-arrow" />
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

defineProps({
  id: {
    type: String,
    default: 'hero'
  }
})

const cvLink = 'src/assets/cv_atualizado.pdf'
const linkedinLink = 'https://www.linkedin.com/in/diego-rodrigues-500b0081/'
const githubLink = 'https://github.com/diegodevweb'

const mainStack = [
  { name: 'Laravel', color: 'red-8', icon: null },
  { name: 'Vue 2/3', color: 'green-7', icon: null },
  { name: 'Git', color: 'blue-7', icon: null },
  { name: 'PostgreSQL', color: 'blue-9', icon: null },
  { name: 'Docker', color: 'blue-6', icon: null },
  { name: 'Redis', color: 'red-7', icon: null }
]

// Typing effect
const texts = [
  'Desenvolvedor Fullstack',
  'Especialista em Laravel & Vue.js',
  'Integrações complexas e APIs',
  'De sites a sistemas empresariais',
]
const typingText = ref('')
let textIndex = 0
let charIndex = 0
let isDeleting = false

const typeEffect = () => {
  const currentText = texts[textIndex] ?? texts[0] ?? ''

  if (isDeleting) {
    typingText.value = currentText.substring(0, charIndex - 1)
    charIndex--
  } else {
    typingText.value = currentText.substring(0, charIndex + 1)
    charIndex++
  }

  let typeSpeed = isDeleting ? 50 : 100

  if (!isDeleting && charIndex === currentText.length) {
    typeSpeed = 2000
    isDeleting = true
  } else if (isDeleting && charIndex === 0) {
    isDeleting = false
    textIndex = (textIndex + 1) % texts.length
    typeSpeed = 500
  }

  setTimeout(typeEffect, typeSpeed)
}

// Particle positions
const getParticleStyle = () => {
  const size = Math.random() * 4 + 2
  return {
    width: `${size}px`,
    height: `${size}px`,
    left: `${Math.random() * 100}%`,
    top: `${Math.random() * 100}%`,
    animationDelay: `${Math.random() * 20}s`,
    animationDuration: `${Math.random() * 10 + 15}s`
  }
}

onMounted(() => {
  typeEffect()
})
</script>

<style scoped lang="scss">
.hero-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  position: relative;
  padding-top: 80px;
}

.container {
  max-width: 1400px;
  margin: 0 auto;
  width: 100%;
  padding-left: 48px;
  padding-right: 48px;
}

// Background grid effect
.hero-grid-bg {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(0, 129, 75, 0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0, 129, 75, 0.03) 1px, transparent 1px);
  background-size: 50px 50px;
  animation: gridMove 20s linear infinite;
}

@keyframes gridMove {
  0% {
    background-position: 0 0;
  }
  100% {
    background-position: 50px 50px;
  }
}

// Particles
.particles-container {
  position: absolute;
  inset: 0;
  overflow: hidden;
  pointer-events: none;
}

.particle {
  position: absolute;
  background: rgba(0, 129, 75, 0.4);
  border-radius: 50%;
  animation: float linear infinite;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0) translateX(0);
    opacity: 0;
  }
  10% {
    opacity: 1;
  }
  90% {
    opacity: 1;
  }
  100% {
    transform: translateY(-100vh) translateX(50px);
    opacity: 0;
  }
}

// Typography
.hero-title {
  font-size: clamp(2rem, 5vw, 3.5rem);
  line-height: 1.2;
  margin-bottom: 1rem;

  .text-primary {
    background: linear-gradient(135deg, #00814b 0%, #00c775 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }
}

.hero-subtitle {
  min-height: 40px;
  font-weight: 500;
}

.typing-text {
  display: inline-block;
}

.typing-cursor {
  display: inline-block;
  animation: blink 1s infinite;
  color: #00814b;
}

@keyframes blink {
  0%, 49% {
    opacity: 1;
  }
  50%, 100% {
    opacity: 0;
  }
}

.letter-spacing {
  letter-spacing: 2px;
}

// Stats cards
.stat-card {
  min-width: 100px;
  transition: all 0.3s ease;
  border: 1px solid rgba(0, 129, 75, 0.2);

  &:hover {
    transform: translateY(-4px);
    border-color: rgba(0, 129, 75, 0.5);
    box-shadow: 0 8px 16px rgba(0, 129, 75, 0.2);
  }
}

// Buttons
.cta-button-primary {
  transition: all 0.3s ease;

  &:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 20px rgba(0, 129, 75, 0.4);
  }
}

.cta-button-secondary {
  transition: all 0.3s ease;

  &:hover {
    transform: translateY(-2px);
    background: rgba(255, 255, 255, 0.05);
  }
}

.social-button {
  transition: all 0.3s ease;

  &:hover {
    transform: scale(1.1);
    background: rgba(0, 129, 75, 0.1);
  }
}

// Hero Card
.hero-card {
  position: relative;
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.4s ease;

  &:hover {
    transform: translateY(-8px);
    border-color: rgba(0, 129, 75, 0.5);

    .gradient-border {
      opacity: 1;
    }

    .avatar-ring {
      transform: scale(1.1) rotate(180deg);
    }
  }
}

.gradient-border {
  position: absolute;
  inset: -2px;
  background: linear-gradient(135deg, #00814b, #00c775, #00814b);
  border-radius: inherit;
  z-index: -1;
  opacity: 0;
  transition: opacity 0.4s ease;
  animation: gradientRotate 3s linear infinite;
}

@keyframes gradientRotate {
  0% {
    filter: hue-rotate(0deg);
  }
  100% {
    filter: hue-rotate(360deg);
  }
}

// Avatar
.avatar-container {
  position: relative;
  display: inline-block;
}

.avatar-main {
  position: relative;
  z-index: 2;
  border: 3px solid #00814b;
}

.avatar-ring {
  position: absolute;
  inset: -8px;
  border: 2px solid rgba(0, 129, 75, 0.3);
  border-radius: 50%;
  transition: all 0.6s ease;
}

.status-badge {
  position: absolute;
  bottom: 0;
  right: -10px;
  padding: 4px 12px;
  border-radius: 20px;
  display: flex;
  align-items: center;
  z-index: 3;
  border: 2px solid #1e1e1e;
}

// Stack chips
.stack-chip {
  transition: all 0.3s ease;

  &:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
  }
}

// Card decorations
.card-decoration {
  position: absolute;
  width: 100px;
  height: 100px;
  border-radius: 50%;
  filter: blur(40px);
  opacity: 0.15;
  pointer-events: none;
}

.card-decoration-1 {
  background: #00814b;
  top: -50px;
  right: -50px;
}

.card-decoration-2 {
  background: #00c775;
  bottom: -50px;
  left: -50px;
}

// Floating badges
.floating-badges {
  position: relative;
  margin-top: -30px;
}

.floating-badge {
  position: absolute;
  animation: floatBadge 3s ease-in-out infinite;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
  font-weight: 600;
}

.badge-1 {
  right: -20px;
  top: -80px;
  animation-delay: 0s;
}

.badge-2 {
  left: -20px;
  top: 40px;
  animation-delay: 1.5s;
}

@keyframes floatBadge {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

// Scroll indicator
.scroll-indicator {
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);
  cursor: pointer;
  z-index: 10;
}

.scroll-arrow {
  animation: bounce 2s infinite;
  color: rgba(255, 255, 255, 0.5);
  transition: color 0.3s ease;

  &:hover {
    color: #00814b;
  }
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateY(0);
  }
  40% {
    transform: translateY(-10px);
  }
  60% {
    transform: translateY(-5px);
  }
}

// Responsive
@media (max-width: 1023px) {
  .container {
    padding-left: 24px;
    padding-right: 24px;
  }

  .floating-badges {
    display: none;
  }

  .hero-title {
    font-size: 2rem;
  }
}
</style>
