<template>
  <section :id="id" class="about-section">
    <div class="container">
      <!-- Section Header -->
      <div class="text-center q-mb-xl" data-aos="fade-up">
        <div class="text-h5 text-primary text-weight-bold">Conheça mais</div>
        <h2 class="text-h3 text-weight-bold q-mb-sm">Sobre mim</h2>
        <p class="text-body1 text-grey-4" style="max-width: 600px; margin: 0 auto;">
          Mais de 3 anos transformando ideias em sistemas que funcionam
        </p>
      </div>

      <div class="row q-col-gutter-xl">
        <!-- Left side - Main content -->
        <div class="col-12 col-md-7" data-aos="fade-right">
          <div class="about-content">
            <p class="text-body1 text-grey-3 q-mb-md" style="line-height: 1.8;">
              Sou desenvolvedor <strong class="text-white">Full Stack</strong> especializado em resolver
              problemas complexos através de código. Minha especialidade é criar sistemas que vão além
              de simples websites: <strong class="text-primary">ERPs, plataformas transacionais,
              integrações fiscais e dashboards administrativos</strong> que realmente fazem diferença
              no dia a dia das empresas.
            </p>

            <p class="text-body1 text-grey-3 q-mb-md" style="line-height: 1.8;">
              Trabalho com <strong class="text-white">Laravel</strong> no back-end e
              <strong class="text-white">Vue.js</strong> no front-end, sempre focado em
              <strong class="text-primary">performance, segurança e manutenibilidade</strong>.
              Tenho experiência desde a modelagem de banco de dados até a criação de interfaces
              ricas e responsivas.
            </p>

            <p class="text-body1 text-grey-3 q-mb-lg" style="line-height: 1.8;">
              Já atuei em projetos desafiadores como <strong class="text-white">emissão de notas
              fiscais eletrônicas (NFe/NFC-e)</strong>, automação com web scraping, plataformas de
              jogos online, e sistemas multi-empresa com integrações complexas.
            </p>

            <!-- Key strengths -->
            <div class="strengths-grid q-mb-lg">
              <div
                v-for="(strength, index) in strengths"
                :key="index"
                class="strength-item"
                data-aos="fade-up"
                :data-aos-delay="index * 100"
              >
                <q-icon :name="strength.icon" size="32px" class="text-primary q-mb-sm" />
                <div class="text-subtitle2 text-weight-bold q-mb-xs">{{ strength.title }}</div>
                <div class="text-caption text-grey-4">{{ strength.description }}</div>
              </div>
            </div>
          </div>
        </div>

        <!-- Right side - Info cards -->
        <div class="col-12 col-md-5" data-aos="fade-left" data-aos-delay="200">
          <!-- Main info card -->
          <q-card flat class="info-card bg-grey-9 rounded-borders q-mb-md">
            <q-card-section class="q-pa-lg">
              <div class="row items-center q-mb-md">
                <q-icon name="code" size="32px" class="text-primary q-mr-sm" />
                <div class="text-h6 text-weight-bold">Stack Principal</div>
              </div>

              <div class="stack-list">
                <div
                  v-for="(item, index) in mainStack"
                  :key="index"
                  class="stack-item"
                >
                  <div class="row items-center justify-between">
                    <div class="text-body2 text-weight-medium">{{ item.name }}</div>
                    <q-badge :color="item.color"/>
                  </div>
                </div>
              </div>
            </q-card-section>
          </q-card>

          <!-- Experience card -->
          <q-card flat class="info-card bg-grey-9 rounded-borders q-mb-md">
            <q-card-section class="q-pa-lg">
              <div class="row items-center q-mb-md">
                <q-icon name="workspace_premium" size="32px" class="text-primary q-mr-sm" />
                <div class="text-h6 text-weight-bold">Experiência</div>
              </div>

              <q-list dense>
                <q-item class="q-px-none">
                  <q-item-section avatar>
                    <q-avatar color="primary" text-color="white" size="40px">
                      <q-icon name="schedule" />
                    </q-avatar>
                  </q-item-section>
                  <q-item-section>
                    <q-item-label class="text-weight-medium">+4 anos</q-item-label>
                    <q-item-label caption class="text-grey-4">Desenvolvimento Web</q-item-label>
                  </q-item-section>
                </q-item>

                <q-item class="q-px-none">
                  <q-item-section avatar>
                    <q-avatar color="green-7" text-color="white" size="40px">
                      <q-icon name="business" />
                    </q-avatar>
                  </q-item-section>
                  <q-item-section>
                    <q-item-label class="text-weight-medium">5+ empresas</q-item-label>
                    <q-item-label caption class="text-grey-4">Claro, BetSolve, Attimo, etc</q-item-label>
                  </q-item-section>
                </q-item>

                <q-item class="q-px-none">
                  <q-item-section avatar>
                    <q-avatar color="blue-7" text-color="white" size="40px">
                      <q-icon name="laptop" />
                    </q-avatar>
                  </q-item-section>
                  <q-item-section>
                    <q-item-label class="text-weight-medium">15+ projetos</q-item-label>
                    <q-item-label caption class="text-grey-4">Entregues com sucesso</q-item-label>
                  </q-item-section>
                </q-item>
              </q-list>
            </q-card-section>
          </q-card>

          <!-- Focus areas card -->
          <q-card flat class="info-card bg-grey-9 rounded-borders">
            <q-card-section class="q-pa-lg">
              <div class="row items-center q-mb-md">
                <q-icon name="book" size="32px" class="text-primary q-mr-sm" />
                <div class="text-h6 text-weight-bold">Especialidades</div>
              </div>

              <div class="specialties-list">
                <q-chip
                  v-for="specialty in specialties"
                  :key="specialty"
                  color="grey-8"
                  text-color="grey-3"
                  size="md"
                  class="specialty-chip"
                >
                  <q-icon name="check_circle" size="16px" class="q-mr-xs text-primary" />
                  {{ specialty }}
                </q-chip>
              </div>
            </q-card-section>
          </q-card>
        </div>
      </div>

      <!-- Bottom stats section -->
      <div class="stats-section q-mt-xl" data-aos="fade-up">
        <div class="row q-col-gutter-lg text-center">
          <div
            v-for="(stat, index) in stats"
            :key="index"
            class="col-12 col-sm-6 col-md-3"
          >
            <q-card flat class="stat-card bg-grey-9">
              <q-card-section>
                <q-icon :name="stat.icon" size="48px" :class="`text-${stat.color}`" class="q-mb-sm" />
                <div class="text-h4 text-weight-bold text-primary counter-value">
                  {{ stat.value }}
                </div>
                <div class="text-body2 text-grey-4">{{ stat.label }}</div>
              </q-card-section>
            </q-card>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
defineProps({
  id: {
    type: String,
    default: 'about'
  }
})

const strengths = [
  {
    icon: 'bolt',
    title: 'Performance',
    description: 'Código otimizado com queries eficientes e cache estratégico'
  },
  {
    icon: 'security',
    title: 'Segurança',
    description: 'Seguindo boas práticas OWASP e validações robustas'
  },
  {
    icon: 'architecture',
    title: 'Arquitetura',
    description: 'Design patterns e código limpo para fácil manutenção'
  },
  {
    icon: 'hub',
    title: 'Integrações',
    description: 'APIs REST, SEFAZ, pagamentos e sistemas legados'
  }
]

const mainStack = [
  { name: 'Laravel / PHP', progress: 0.95, color: 'red-8' },
  { name: 'Vue.js / Quasar', progress: 0.90, color: 'green-7' },
  { name: 'PostgreSQL / MySQL', progress: 0.85, color: 'blue-7' },
  { name: 'Docker / Redis', progress: 0.70, color: 'blue-6' },
  { name: 'Git / CI/CD', progress: 0.80, color: 'orange-7' }
]

const specialties = [
  'Integrações NFe/SEFAZ',
  'APIs REST',
  'Filas e Jobs',
  'Multi-tenancy',
  'Web Scraping',
  'Dashboards Admin',
  'Gateways de Pagamento',
  'Sistemas Transacionais'
]

const stats = [
  { icon: 'workspace_premium', value: '4+', label: 'Anos de experiência', color: 'primary' },
  { icon: 'code', value: '15+', label: 'Projetos entregues', color: 'green-7' },
  { icon: 'business', value: '5+', label: 'Empresas', color: 'blue-7' },
  { icon: 'integration_instructions', value: '20+', label: 'Integrações', color: 'orange-7' }
]
</script>

<style scoped lang="scss">
.about-section {
  padding: 80px 0;
  position: relative;
}

.container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 48px;
}

// Content
.about-content {
  p {
    strong {
      font-weight: 600;
    }
  }
}

// Strengths grid
.strengths-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 24px;
}

.strength-item {
  padding: 24px;
  background: rgba(0, 129, 75, 0.05);
  border-radius: 12px;
  border: 1px solid rgba(0, 129, 75, 0.1);
  transition: all 0.3s ease;

  &:hover {
    transform: translateY(-4px);
    background: rgba(0, 129, 75, 0.1);
    border-color: rgba(0, 129, 75, 0.3);
    box-shadow: 0 8px 16px rgba(0, 129, 75, 0.2);
  }
}

// Info cards
.info-card {
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;

  &:hover {
    transform: translateY(-4px);
    border-color: rgba(0, 129, 75, 0.3);
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
  }
}

// Stack list
.stack-list {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.stack-item {
  padding: 12px;
  background: rgba(255, 255, 255, 0.02);
  border-radius: 8px;
  transition: all 0.3s ease;

  &:hover {
    background: rgba(255, 255, 255, 0.05);
    transform: translateX(4px);
  }
}

// Specialties
.specialties-list {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.specialty-chip {
  transition: all 0.3s ease;

  &:hover {
    transform: scale(1.05);
    background: rgba(0, 129, 75, 0.2) !important;
  }
}

// Stats section
.stats-section {
  padding: 40px 0;
}

.stat-card {
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
  cursor: default;

  &:hover {
    transform: translateY(-8px);
    border-color: rgba(0, 129, 75, 0.3);
    box-shadow: 0 12px 24px rgba(0, 0, 0, 0.3);

    .counter-value {
      transform: scale(1.1);
    }
  }
}

.counter-value {
  transition: transform 0.3s ease;
}

// Responsive
@media (max-width: 1023px) {
  .container {
    padding: 0 24px;
  }

  .about-section {
    padding: 60px 0;
  }

  .strengths-grid {
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 16px;
  }
}

@media (max-width: 599px) {
  .strengths-grid {
    grid-template-columns: 1fr;
  }
}
</style>
