<template>
  <section :id="id" class="skills-section">
    <div class="container">
      <!-- Section Header -->
      <div class="text-center q-mb-xl" data-aos="fade-up">
        <div class="text-h5 text-primary text-weight-bold">Competências</div>
        <h2 class="text-h3 text-weight-bold q-mb-sm">Skills & Tecnologias</h2>
        <p class="text-body1 text-grey-4" style="max-width: 600px; margin: 0 auto;">
          Ferramentas e tecnologias que domino para criar soluções completas
        </p>
      </div>

      <!-- Main skills with progress bars -->
      <div class="row q-col-gutter-xl q-mb-xl">
        <!-- Backend -->
        <div class="col-12 col-md-6" data-aos="fade-right">
          <q-card flat class="skill-category-card bg-grey-9">
            <q-card-section class="q-pa-lg">
              <div class="category-header q-mb-lg">
                <div class="row items-center">
                  <q-avatar size="56px" class="category-icon bg-red-9">
                    <q-icon name="dns" size="32px" class="text-red-3" />
                  </q-avatar>
                  <div class="q-ml-md">
                    <div class="text-h5 text-weight-bold">Backend</div>
                    <div class="text-caption text-grey-4">Servidor, APIs e Banco de Dados</div>
                  </div>
                </div>
              </div>

              <div class="skills-list">
                <div
                  v-for="(skill, index) in backendSkills"
                  :key="skill.name"
                  class="skill-item"
                  data-aos="fade-up"
                  :data-aos-delay="index * 50"
                >
                  <div class="row items-center justify-between q-mb-xs">
                    <div class="skill-name">
                      <q-icon :name="skill.icon" size="20px" :class="`text-${skill.color}`" class="q-mr-sm" />
                      <span class="text-body1 text-weight-medium">{{ skill.name }}</span>
                    </div>
                  </div>
                  <div class="text-caption text-grey-5 q-mt-xs">{{ skill.description }}</div>
                </div>
              </div>
            </q-card-section>
          </q-card>
        </div>

        <!-- Frontend -->
        <div class="col-12 col-md-6" data-aos="fade-left">
          <q-card flat class="skill-category-card bg-grey-9">
            <q-card-section class="q-pa-lg">
              <div class="category-header q-mb-lg">
                <div class="row items-center">
                  <q-avatar size="56px" class="category-icon bg-green-9">
                    <q-icon name="web" size="32px" class="text-green-3" />
                  </q-avatar>
                  <div class="q-ml-md">
                    <div class="text-h5 text-weight-bold">Frontend</div>
                    <div class="text-caption text-grey-4">Interface e Experiência do Usuário</div>
                  </div>
                </div>
              </div>

              <div class="skills-list">
                <div
                  v-for="(skill, index) in frontendSkills"
                  :key="skill.name"
                  class="skill-item"
                  data-aos="fade-up"
                  :data-aos-delay="index * 50"
                >
                  <div class="row items-center justify-between q-mb-xs">
                    <div class="skill-name">
                      <q-icon :name="skill.icon" size="20px" :class="`text-${skill.color}`" class="q-mr-sm" />
                      <span class="text-body1 text-weight-medium">{{ skill.name }}</span>
                    </div>
                  </div>
                  <div class="text-caption text-grey-5 q-mt-xs">{{ skill.description }}</div>
                </div>
              </div>
            </q-card-section>
          </q-card>
        </div>
      </div>

      <!-- Additional skills grid -->
      <div class="row q-col-gutter-lg q-mb-xl">
        <!-- DevOps & Tools -->
        <div class="col-12 col-md-4" data-aos="fade-up" data-aos-delay="100">
          <q-card flat class="secondary-skill-card bg-grey-9 full-height">
            <q-card-section class="q-pa-lg">
              <div class="row items-center q-mb-md">
                <q-avatar size="48px" class="bg-blue-9">
                  <q-icon name="settings" size="28px" class="text-blue-3" />
                </q-avatar>
                <div class="q-ml-md">
                  <div class="text-h6 text-weight-bold">DevOps & Tools</div>
                </div>
              </div>

              <q-list dense>
                <q-item v-for="tool in devopsTools" :key="tool.name" class="q-px-none skill-list-item">
                  <q-item-section avatar style="min-width: 40px;">
                    <q-icon :name="tool.icon" size="24px" :class="`text-${tool.color}`" />
                  </q-item-section>
                  <q-item-section>
                    <q-item-label class="text-weight-medium">{{ tool.name }}</q-item-label>
                    <q-item-label caption>{{ tool.use }}</q-item-label>
                  </q-item-section>
                  <q-item-section side>
                    <q-icon name="check_circle" size="18px" class="text-positive" />
                  </q-item-section>
                </q-item>
              </q-list>
            </q-card-section>
          </q-card>
        </div>

        <!-- Specialties -->
        <div class="col-12 col-md-4" data-aos="fade-up" data-aos-delay="200">
          <q-card flat class="secondary-skill-card bg-grey-9 full-height">
            <q-card-section class="q-pa-lg">
              <div class="row items-center q-mb-md">
                <q-avatar size="48px" class="bg-purple-9">
                  <q-icon name="star" size="28px" class="text-purple-3" />
                </q-avatar>
                <div class="q-ml-md">
                  <div class="text-h6 text-weight-bold">Especialidades</div>
                </div>
              </div>

              <div class="specialties-grid">
                <q-chip
                  v-for="specialty in specialties"
                  :key="specialty.name"
                  :color="specialty.color"
                  text-color="white"
                  size="md"
                  class="specialty-chip"
                >
                  <q-icon :name="specialty.icon" size="16px" class="q-mr-xs" />
                  {{ specialty.name }}
                </q-chip>
              </div>
            </q-card-section>
          </q-card>
        </div>

        <!-- Learning -->
        <div class="col-12 col-md-4" data-aos="fade-up" data-aos-delay="300">
          <q-card flat class="secondary-skill-card bg-grey-9 full-height">
            <q-card-section class="q-pa-lg">
              <div class="row items-center q-mb-md">
                <q-avatar size="48px" class="bg-orange-9">
                  <q-icon name="school" size="28px" class="text-orange-3" />
                </q-avatar>
                <div class="q-ml-md">
                  <div class="text-h6 text-weight-bold">Aprendendo</div>
                </div>
              </div>

              <q-list dense>
                <q-item v-for="item in learning" :key="item.name" class="q-px-none skill-list-item">
                  <q-item-section avatar style="min-width: 40px;">
                    <q-icon :name="item.icon" size="24px" class="text-orange-7" />
                  </q-item-section>
                  <q-item-section>
                    <q-item-label class="text-weight-medium">{{ item.name }}</q-item-label>
                    <q-item-label caption>{{ item.reason }}</q-item-label>
                  </q-item-section>
                </q-item>
              </q-list>
            </q-card-section>
          </q-card>
        </div>
      </div>

      <!-- Soft Skills -->
      <div class="soft-skills-section" data-aos="fade-up">
        <q-card flat class="bg-grey-9">
          <q-card-section class="q-pa-lg">
            <div class="text-center q-mb-lg">
              <div class="text-h5 text-weight-bold q-mb-sm">Soft Skills</div>
              <div class="text-body2 text-grey-4">Habilidades interpessoais e profissionais</div>
            </div>

            <div class="row q-col-gutter-md">
              <div
                v-for="(skill) in softSkills"
                :key="skill.name"
                class="col-6 col-sm-4 col-md-3"
              >
                <div class="soft-skill-card text-center">
                  <q-avatar size="64px" :class="`bg-${skill.color}-9`" class="q-mb-sm">
                    <q-icon :name="skill.icon" size="32px" :class="`text-${skill.color}-3`" />
                  </q-avatar>
                  <div class="text-body2 text-weight-medium">{{ skill.name }}</div>
                  <div class="text-caption text-grey-5">{{ skill.description }}</div>
                </div>
              </div>
            </div>
          </q-card-section>
        </q-card>
      </div>

      <!-- Stats footer -->
      <div class="stats-footer q-mt-xl" data-aos="fade-up">
        <div class="row q-col-gutter-md text-center">
          <div v-for="stat in stats" :key="stat.label" class="col-6 col-sm-3">
            <div class="stat-item">
              <q-icon :name="stat.icon" size="40px" :class="`text-${stat.color}`" class="q-mb-sm" />
              <div class="text-h4 text-weight-bold text-primary">{{ stat.value }}</div>
              <div class="text-caption text-grey-4">{{ stat.label }}</div>
            </div>
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
    default: 'skills'
  }
})

const backendSkills = [
  {
    name: 'PHP / Laravel',
    icon: 'code',
    color: 'red-7',
    description: 'Framework principal, patterns avançados, otimizações'
  },
  {
    name: 'APIs REST',
    icon: 'api',
    color: 'blue-7',
    description: 'Design, documentação, versionamento e segurança'
  },
  {
    name: 'PostgreSQL / MySQL',
    icon: 'storage',
    color: 'blue-8',
    description: 'Modelagem, otimização de queries, índices'
  },
  {
    name: 'Redis / Queues',
    icon: 'flash_on',
    color: 'red-8',
    description: 'Cache, jobs assíncronos, filas de processamento'
  },
  {
    name: 'Integrações',
    icon: 'hub',
    color: 'purple-7',
    description: 'SEFAZ, pagamentos, APIs externas, webhooks'
  }
]

const frontendSkills = [
  {
    name: 'Vue.js 3',
    icon: 'javascript',
    color: 'green-7',
    description: 'Composition API, componentes reutilizáveis, estado'
  },
  {
    name: 'Quasar Framework',
    icon: 'widgets',
    color: 'blue-7',
    description: 'Componentes, layouts, responsividade'
  },
  {
    name: 'Vuetify',
    icon: 'palette',
    color: 'blue-8',
    description: 'Material Design, components, theming'
  },
  {
    name: 'Alpine.js',
    icon: 'code',
    color: 'cyan-7',
    description: 'Interatividade leve em Blade/Livewire'
  },
  {
    name: 'HTML/CSS/JS',
    icon: 'web',
    color: 'orange-7',
    description: 'Fundamentos sólidos, responsividade, acessibilidade'
  }
]

const devopsTools = [
  { name: 'Git / GitHub', icon: 'mdi-git', color: 'orange-7', use: 'Versionamento e colaboração' },
  { name: 'Docker', icon: 'mdi-docker', color: 'blue-6', use: 'Containerização e ambientes' },
  { name: 'Linux / Ubuntu', icon: 'terminal', color: 'grey-6', use: 'Servidores e deploy' },
  { name: 'Composer / NPM', icon: 'terminal', color: 'red-7', use: 'Gerenciamento de dependências' },
  { name: 'Postman / Swagger', icon: 'description', color: 'orange-6', use: 'Testes e documentação APIs' }
]

const specialties = [
  { name: 'NFe/NFC-e', icon: 'receipt_long', color: 'purple-7' },
  { name: 'Multi-tenancy', icon: 'business', color: 'blue-7' },
  { name: 'Web Scraping', icon: 'travel_explore', color: 'pink-7' },
  { name: 'Payments', icon: 'payment', color: 'green-7' },
  { name: 'Jobs/Queues', icon: 'schedule', color: 'orange-7' },
  { name: 'Dashboards', icon: 'dashboard', color: 'cyan-7' },
  { name: 'Auth/JWT', icon: 'lock', color: 'red-7' },
  { name: 'Filament', icon: 'admin_panel_settings', color: 'amber-7' }
]

const learning = [
  { name: 'TypeScript', icon: 'code', reason: 'Tipagem estática para Vue' },
  { name: 'Testing (PHPUnit)', icon: 'bug_report', reason: 'Testes automatizados' },
  { name: 'Kafka', icon: 'code', reason: 'Streaming de dados em tempo real' },
  { name: 'CI/CD', icon: 'sync', reason: 'Deploy automatizado' },
  { name: 'GraphQL', icon: 'api', reason: 'APIs flexíveis' }
]

const softSkills = [
  { name: 'Comunicação', icon: 'chat', color: 'green', description: 'Stakeholders e clientes' },
  { name: 'Resolução de Problemas', icon: 'lightbulb', color: 'orange', description: 'Soluções criativas' },
  { name: 'Metodologias Ágeis', icon: 'speed', color: 'purple', description: 'SCRUM e Kanban' },
  { name: 'Trabalho Remoto', icon: 'home', color: 'cyan', description: 'Autonomia e disciplina' },
  { name: 'Code Review', icon: 'rate_review', color: 'pink', description: 'Qualidade de código' },
  { name: 'Documentação', icon: 'description', color: 'indigo', description: 'Clara e completa' },
  { name: 'Mentoria', icon: 'school', color: 'teal', description: 'Ensinar e compartilhar' }
]

const stats = [
  { icon: 'code', value: '10+', label: 'Tecnologias', color: 'primary' },
  { icon: 'library_books', value: '20+', label: 'Bibliotecas', color: 'blue-7' },
  { icon: 'integration_instructions', value: '15+', label: 'Integrações', color: 'purple-7' },
  { icon: 'emoji_events', value: '8+', label: 'Especialidades', color: 'orange-7' }
]
</script>

<style scoped lang="scss">
.skills-section {
  padding: 80px 0;
  background: linear-gradient(180deg, rgba(0, 129, 75, 0.02) 0%, transparent 50%, rgba(0, 129, 75, 0.02) 100%);
}

.container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 48px;
}

// Skill category cards
.skill-category-card {
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 16px;
  transition: all 0.4s ease;

  &:hover {
    transform: translateY(-8px);
    border-color: rgba(0, 129, 75, 0.3);
    box-shadow: 0 16px 32px rgba(0, 0, 0, 0.3);
  }
}

.category-header {
  .category-icon {
    transition: transform 0.3s ease;
  }

  &:hover .category-icon {
    transform: scale(1.1) rotate(5deg);
  }
}

// Skills list
.skills-list {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.skill-item {
  padding: 16px;
  background: rgba(255, 255, 255, 0.02);
  border-radius: 12px;
  border: 1px solid transparent;
  transition: all 0.3s ease;

  &:hover {
    background: rgba(255, 255, 255, 0.05);
    border-color: rgba(0, 129, 75, 0.2);
    transform: translateX(8px);
  }
}

.skill-name {
  display: flex;
  align-items: center;
}

.skill-progress {
  transition: all 0.3s ease;

  :deep(.q-linear-progress__track) {
    opacity: 0.3;
  }
}

// Secondary cards
.secondary-skill-card {
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 16px;
  transition: all 0.3s ease;

  &:hover {
    transform: translateY(-4px);
    border-color: rgba(0, 129, 75, 0.3);
    box-shadow: 0 12px 24px rgba(0, 0, 0, 0.3);
  }
}

.skill-list-item {
  padding: 12px;
  margin-bottom: 8px;
  background: rgba(255, 255, 255, 0.02);
  border-radius: 8px;
  transition: all 0.3s ease;

  &:hover {
    background: rgba(255, 255, 255, 0.05);
    transform: translateX(4px);
  }
}

// Specialties
.specialties-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.specialty-chip {
  transition: all 0.3s ease;
  cursor: default;

  &:hover {
    transform: scale(1.05);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
  }
}

// Soft skills
.soft-skills-section {
  :deep(.q-card) {
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 16px;
  }
}

.soft-skill-card {
  padding: 20px;
  background: rgba(255, 255, 255, 0.02);
  border-radius: 12px;
  transition: all 0.3s ease;
  cursor: default;

  &:hover {
    background: rgba(255, 255, 255, 0.05);
    transform: translateY(-4px);

    .q-avatar {
      transform: scale(1.1);
    }
  }

  .q-avatar {
    transition: transform 0.3s ease;
  }
}

// Stats footer
.stats-footer {
  padding: 40px 0;
}

.stat-item {
  padding: 24px;
  background: rgba(255, 255, 255, 0.02);
  border-radius: 12px;
  transition: all 0.3s ease;
  cursor: default;

  &:hover {
    background: rgba(0, 129, 75, 0.1);
    transform: translateY(-4px);
  }
}

// Responsive
@media (max-width: 1023px) {
  .container {
    padding: 0 24px;
  }

  .skills-section {
    padding: 60px 0;
  }
}

@media (max-width: 599px) {
  .skills-list {
    gap: 16px;
  }

  .skill-item {
    padding: 12px;
  }

  .soft-skill-card {
    padding: 16px;
  }
}
</style>
