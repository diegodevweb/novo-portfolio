<template>
  <section :id="id" class="projects-section">
    <div class="container">
      <!-- Section Header -->
      <div class="text-center q-mb-xl" data-aos="fade-up">
        <div class="text-h5 text-primary text-weight-bold">Portfolio</div>
        <h2 class="text-h3 text-weight-bold q-mb-sm">Projetos em Destaque</h2>
        <p class="text-body1 text-grey-4" style="max-width: 600px; margin: 0 auto;">
          Seleção de projetos complexos que demonstram expertise técnica e impacto real
        </p>
      </div>

      <!-- Filter buttons -->
      <div class="text-center q-mb-lg" data-aos="fade-up" data-aos-delay="100">
        <q-btn-group flat>
          <q-btn
            v-for="category in categories"
            :key="category.value"
            :label="category.label"
            :outline="selectedCategory !== category.value"
            :unelevated="selectedCategory === category.value"
            :color="selectedCategory === category.value ? 'primary' : 'grey-7'"
            @click="selectedCategory = category.value"
            class="filter-btn"
          >
            <q-icon :name="category.icon" size="18px" class="q-mr-xs" />
          </q-btn>
        </q-btn-group>
      </div>

      <!-- Projects Grid -->
      <div class="row q-col-gutter-lg">
        <div
          v-for="(project, index) in filteredProjects"
          :key="project.id"
          class="col-12 col-md-6 col-lg-4"
          data-aos="fade-up"
          :data-aos-delay="index * 100"
        >
          <q-card
            flat
            class="project-card bg-grey-9 full-height column cursor-pointer"
            @click="openProjectModal(project)"
          >
            <!-- Project thumbnail/icon -->
            <div class="project-thumbnail" :style="{ background: project.gradient }">
              <q-icon :name="project.icon" size="64px" class="text-white" />
              <div class="thumbnail-overlay">
                <q-btn
                  round
                  color="white"
                  text-color="grey-10"
                  icon="visibility"
                  size="md"
                />
              </div>
            </div>

            <q-card-section class="column q-pa-lg" style="flex: 1;">
              <!-- Category badge -->
              <q-badge
                :color="getCategoryColor(project.category)"
                :label="getCategoryLabel(project.category)"
                class="q-mb-sm"
              />

              <!-- Title -->
              <div class="text-h6 text-weight-bold q-mb-xs">
                {{ project.title }}
              </div>

              <!-- Role -->
              <div class="text-caption text-primary q-mb-sm">
                {{ project.role }}
              </div>

              <!-- Description -->
              <div class="text-body2 text-grey-3 q-mb-md" style="line-height: 1.6;">
                {{ project.shortDescription }}
              </div>

              <!-- Metrics -->
              <div class="metrics-row q-mb-md" v-if="project.metrics">
                <div
                  v-for="metric in project.metrics"
                  :key="metric.label"
                  class="metric-item"
                >
                  <div class="text-h6 text-weight-bold text-primary">{{ metric.value }}</div>
                  <div class="text-caption text-grey-5">{{ metric.label }}</div>
                </div>
              </div>

              <!-- Tech stack -->
              <div class="q-mt-auto">
                <div class="text-caption text-grey-5 q-mb-xs">Stack</div>
                <div class="row q-gutter-xs">
                  <q-chip
                    v-for="tech in project.stack.slice(0, 4)"
                    :key="tech"
                    dense
                    outline
                    color="primary"
                    text-color="primary"
                    size="sm"
                  >
                    {{ tech }}
                  </q-chip>
                  <q-chip
                    v-if="project.stack.length > 4"
                    dense
                    outline
                    color="grey-7"
                    text-color="grey-4"
                    size="sm"
                  >
                    +{{ project.stack.length - 4 }}
                  </q-chip>
                </div>
              </div>
            </q-card-section>

            <!-- Hover effect -->
            <div class="card-shine"></div>
          </q-card>
        </div>
      </div>

      <!-- Empty state -->
      <div v-if="filteredProjects.length === 0" class="text-center q-py-xl">
        <q-icon name="search_off" size="64px" class="text-grey-7 q-mb-md" />
        <div class="text-h6 text-grey-5">Nenhum projeto nesta categoria</div>
      </div>
    </div>

    <!-- Project Detail Modal -->
    <q-dialog v-model="showModal" maximized transition-show="slide-up" transition-hide="slide-down">
      <q-card class="bg-grey-10 text-white" v-if="selectedProject">
        <q-bar class="bg-grey-9">
          <q-space />
          <q-btn dense flat icon="close" v-close-popup>
            <q-tooltip>Fechar</q-tooltip>
          </q-btn>
        </q-bar>

        <q-card-section class="q-pa-none">
          <div class="modal-container">
            <!-- Hero section -->
            <div class="modal-hero" :style="{ background: selectedProject.gradient }">
              <div class="container">
                <div class="row items-center q-py-xl">
                  <div class="col-12 col-md-8">
                    <q-badge
                      :color="getCategoryColor(selectedProject.category)"
                      :label="getCategoryLabel(selectedProject.category)"
                      class="q-mb-md"
                      size="lg"
                    />
                    <h2 class="text-h3 text-weight-bold q-mb-sm">{{ selectedProject.title }}</h2>
                    <div class="text-h6 text-grey-3 q-mb-md">{{ selectedProject.role }}</div>
                    <p class="text-body1" style="max-width: 700px;">
                      {{ selectedProject.fullDescription }}
                    </p>
                  </div>
                  <div class="col-12 col-md-4 text-center">
                    <q-icon :name="selectedProject.icon" size="120px" class="text-white" style="opacity: 0.3;" />
                  </div>
                </div>
              </div>
            </div>

            <!-- Content -->
            <div class="container q-py-xl">
              <div class="row q-col-gutter-xl">
                <!-- Left column -->
                <div class="col-12 col-md-8">
                  <!-- Metrics -->
                  <div class="q-mb-xl" v-if="selectedProject.metrics">
                    <h3 class="text-h5 text-weight-bold q-mb-md">
                      <q-icon name="analytics" class="q-mr-sm text-primary" />
                      Impacto e Resultados
                    </h3>
                    <div class="row q-col-gutter-md">
                      <div
                        v-for="metric in selectedProject.metrics"
                        :key="metric.label"
                        class="col-6 col-sm-3"
                      >
                        <q-card flat class="bg-grey-9 text-center q-pa-md">
                          <div class="text-h4 text-weight-bold text-primary">{{ metric.value }}</div>
                          <div class="text-caption text-grey-4">{{ metric.label }}</div>
                        </q-card>
                      </div>
                    </div>
                  </div>

                  <!-- Key Features -->
                  <div class="q-mb-xl">
                    <h3 class="text-h5 text-weight-bold q-mb-md">
                      <q-icon name="star" class="q-mr-sm text-primary" />
                      Principais Funcionalidades
                    </h3>
                    <q-list>
                      <q-item
                        v-for="(feature, idx) in selectedProject.features"
                        :key="idx"
                        class="q-px-none"
                      >
                        <q-item-section avatar>
                          <q-avatar color="primary" text-color="white" size="32px">
                            <q-icon name="check" />
                          </q-avatar>
                        </q-item-section>
                        <q-item-section>
                          <q-item-label class="text-body1 text-weight-medium">
                            {{ feature }}
                          </q-item-label>
                        </q-item-section>
                      </q-item>
                    </q-list>
                  </div>

                  <!-- Challenges -->
                  <div class="q-mb-xl">
                    <h3 class="text-h5 text-weight-bold q-mb-md">
                      <q-icon name="extension" class="q-mr-sm text-primary" />
                      Desafios Técnicos
                    </h3>
                    <q-list>
                      <q-item
                        v-for="(challenge, idx) in selectedProject.challenges"
                        :key="idx"
                        class="q-px-none"
                      >
                        <q-item-section avatar>
                          <q-icon name="arrow_right" size="24px" class="text-orange-7" />
                        </q-item-section>
                        <q-item-section>
                          <q-item-label class="text-body2 text-grey-3">
                            {{ challenge }}
                          </q-item-label>
                        </q-item-section>
                      </q-item>
                    </q-list>
                  </div>
                </div>

                <!-- Right column - Tech details -->
                <div class="col-12 col-md-4">
                  <!-- Tech Stack -->
                  <q-card flat class="bg-grey-9 q-mb-md">
                    <q-card-section>
                      <div class="text-subtitle1 text-weight-bold q-mb-md">
                        <q-icon name="code" class="q-mr-xs text-primary" />
                        Stack Técnica
                      </div>
                      <div class="stack-tags">
                        <q-chip
                          v-for="tech in selectedProject.stack"
                          :key="tech"
                          color="grey-8"
                          text-color="grey-2"
                          size="md"
                        >
                          {{ tech }}
                        </q-chip>
                      </div>
                    </q-card-section>
                  </q-card>

                  <!-- Project Info -->
                  <q-card flat class="bg-grey-9 q-mb-md">
                    <q-card-section>
                      <div class="text-subtitle1 text-weight-bold q-mb-md">
                        <q-icon name="info" class="q-mr-xs text-primary" />
                        Informações
                      </div>
                      <q-list dense>
                        <q-item class="q-px-none">
                          <q-item-section>
                            <q-item-label caption>Empresa</q-item-label>
                            <q-item-label>{{ selectedProject.company }}</q-item-label>
                          </q-item-section>
                        </q-item>
                        <q-item class="q-px-none">
                          <q-item-section>
                            <q-item-label caption>Período</q-item-label>
                            <q-item-label>{{ selectedProject.period }}</q-item-label>
                          </q-item-section>
                        </q-item>
                        <q-item class="q-px-none">
                          <q-item-section>
                            <q-item-label caption>Tipo</q-item-label>
                            <q-item-label>{{ selectedProject.type }}</q-item-label>
                          </q-item-section>
                        </q-item>
                      </q-list>
                    </q-card-section>
                  </q-card>

                  <!-- Tags -->
                  <q-card flat class="bg-grey-9">
                    <q-card-section>
                      <div class="text-subtitle1 text-weight-bold q-mb-md">
                        <q-icon name="label" class="q-mr-xs text-primary" />
                        Tags
                      </div>
                      <div class="stack-tags">
                        <q-chip
                          v-for="tag in selectedProject.tags"
                          :key="tag"
                          outline
                          color="primary"
                          text-color="primary"
                          size="sm"
                        >
                          {{ tag }}
                        </q-chip>
                      </div>
                    </q-card-section>
                  </q-card>
                </div>
              </div>
            </div>
          </div>
        </q-card-section>
      </q-card>
    </q-dialog>
  </section>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

defineProps({
  id: {
    type: String,
    default: 'projects'
  }
})

const selectedCategory = ref('all')
const showModal = ref(false)
const selectedProject = ref<Project | null>(null)

interface Project {
  id: number
  title: string
  role: string
  shortDescription: string
  fullDescription: string
  category: string
  icon: string
  gradient: string
  company: string
  period: string
  type: string
  stack: string[]
  tags: string[]
  features: string[]
  challenges: string[]
  metrics?: Array<{ value: string; label: string }>
}

const categories = [
  { value: 'all', label: 'Todos', icon: 'apps' },
  { value: 'fiscal', label: 'Fiscal', icon: 'receipt_long' },
  { value: 'automation', label: 'Automação', icon: '' },
  { value: 'api', label: 'APIs', icon: 'api' },
  { value: 'platform', label: 'Plataformas', icon: 'web' }
]

const projects: Project[] = [
  {
    id: 1,
    title: 'Sistema de Emissão de NFe/NFC-e',
    role: 'Full Stack Developer & Full Stack Engineer',
    shortDescription: 'Sistema completo multi-empresa para emissão de notas fiscais eletrônicas com integrações SEFAZ, gestão de certificados digitais e painéis administrativos.',
    fullDescription: 'Implementação completa de sistema fiscal com suporte a múltiplas empresas, emissão de NFe e NFC-e, integração com SEFAZ de vários estados, gestão automática de certificados digitais A1 e A3, importação de produtos e painéis administrativos robustos com Filament.',
    category: 'fiscal',
    icon: 'receipt_long',
    gradient: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
    company: 'Attimo Soluções',
    period: 'Fev/2025 - Out/2025',
    type: 'Enterprise',
    stack: ['Laravel', 'Vue.js', 'Filament', 'MySql', 'Redis', 'Docker', 'SEFAZ API'],
    tags: ['Multi-tenancy', 'Fiscal', 'Integrações', 'Enterprise'],
    features: [
      'Emissão de NFe e NFC-e com validação automática',
      'Integração com SEFAZ SP',
      'Gestão de certificados digitais A1 e A3',
      'Sistema multi-empresa com isolamento de dados',
      'Importação automática de produtos com validações',
      'Painel administrativo completo com Filament',
      'Consulta e cancelamento de notas',
      'Geração e validação de XML',
      'Logs detalhados e auditoria'
    ],
    challenges: [
      'Implementar isolamento perfeito de dados entre empresas',
      'Gerenciar renovação automática de certificados A1 e A3',
      'Lidar com diferentes regras fiscais por estado',
      'Otimizar queries para grande volume de notas',
      'Implementar sistema robusto de retry para integrações SEFAZ',
      'Criar arquitetura escalável para múltiplas empresas',
      'Atuar no desenvolvimento de funcionalidades para atender à nova RTC',
    ],
    metrics: [
      { value: '10+', label: 'Estados' },
      { value: '50+', label: 'Empresas' },
      { value: '5K+', label: 'NFes/mês' },
      { value: '99%', label: 'Uptime' }
    ]
  },
  {
    id: 2,
    title: 'Automação Web Scraping',
    role: 'Fullstack Developer',
    shortDescription: 'Sistema de automação para extração e processamento de dados com jobs assíncronos e tratamento de sessões.',
    fullDescription: 'Desenvolvimento de sistema robusto de web scraping para extrair dados de sistemas legados, com arquitetura de filas para processamento assíncrono, gerenciamento inteligente de sessões e tratamento de falhas.',
    category: 'automation',
    icon: 'smart_toy',
    gradient: 'linear-gradient(135deg, #f093fb 0%, #f5576c 100%)',
    company: 'Claro',
    period: '2025',
    type: 'Enterprise',
    stack: ['Laravel', 'PHP', 'Redis', 'Queues', 'MySQL', 'Guzzle'],
    tags: ['Web Scraping', 'Jobs', 'Automação', 'Legacy Systems', 'Dinamic Tables'],
    features: [
      'Web scraping robusto com tratamento de erros',
      'Sistema de filas para processamento assíncrono',
      'Gerenciamento automático de sessões',
      'Retry automático com backoff exponencial',
      'Logs estruturados e monitoramento',
      'Processamento paralelo de múltiplos registros',
      'Extração e complementação de dados RECs/RALs',
      'Dashboard para acompanhamento de processamento'
    ],
    challenges: [
      'Lidar com sistema legado sem API oficial',
      'Gerenciar expiração de sessões automaticamente',
      'Implementar retry inteligente sem sobrecarregar o sistema',
      'Processar grandes volumes de dados eficientemente',
      'Tratar inconsistências nos dados extraídos',
      'Paralelizar processos mantendo integridade'
    ],
    metrics: [
      { value: '70%', label: 'Redução tempo' },
      { value: '10K+', label: 'Registros/dia' },
      { value: '95%', label: 'Taxa sucesso' },
      { value: '24/7', label: 'Disponível' }
    ]
  },
  {
    id: 3,
    title: 'Plataforma iGaming',
    role: 'Tech Lead & Full Stack (Part time)',
    shortDescription: 'Plataforma completa de apostas esportivas e jogos digitais com sistema transacional, processamento de pagamentos e gestão de prêmios.',
    fullDescription: 'Liderança técnica no desenvolvimento de plataforma de apostas esportivas e jogos online, incluindo integração com gateways de pagamento, sistema de gestão de prêmios e saques, arquitetura para jogos digitais, e implementação de boas práticas de segurança OWASP.',
    category: 'platform',
    icon: 'sports_esports',
    gradient: 'linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)',
    company: 'BetSolve',
    period: 'Jun/2025 - Ago/2025',
    type: 'iGaming',
    stack: ['Laravel', 'Vue.js', 'PostgreSQL', 'Redis', 'Payment APIs', 'WebSockets'],
    tags: ['Gaming', 'Pagamentos', 'Liderança', 'Segurança'],
    features: [
      'Sistema de apostas esportivas em tempo real',
      'Jogo digital Raspadinha com prêmios instantâneos',
      'Integração completa com gateways de pagamento',
      'Sistema de carteira digital',
      'Gestão de prêmios e saques com auditoria',
      'Painel administrativo para operações',
      'Sistema de afiliados e comissões',
      'Relatórios financeiros e compliance'
    ],
    challenges: [
      'Garantir integridade transacional em operações concorrentes',
      'Implementar sistema de prevenção de fraudes',
      'Lidar com alto volume de transações simultâneas',
      'Integrar múltiplos gateways de pagamento (SuitPay, WorldPayments, Xgate, StarkBank)',
      'Implementar RNG (Random Number Generator) certificável',
      'Garantir compliance com regulamentações de jogos'
    ],
    metrics: [
      { value: '5K+', label: 'Usuários' },
      { value: '100K+', label: 'Transações' },
      { value: 'OWASP', label: 'Segurança' }
    ]
  },
  {
    id: 4,
    title: 'API REST para Mobile',
    role: 'Backend Developer',
    shortDescription: 'Desenvolvimento de API REST completa documentada com Swagger, sistema de notificações push e automações com cronjobs e listeners.',
    fullDescription: 'Criação de APIs REST robustas para aplicativo mobile Clube de Férias, com documentação completa em Swagger, implementação de sistema de notificações push em tempo real, autenticação JWT, cronjobs para automações e listeners para processos de negócio.',
    category: 'api',
    icon: 'api',
    gradient: 'linear-gradient(135deg, #a8edea 0%, #fed6e3 100%)',
    company: 'Grupo Águia',
    period: 'Out/2023 - Ago/2024',
    type: 'API Backend',
    stack: ['Laravel', 'Swagger', 'JWT', 'MySQL', 'Redis', 'FCM'],
    tags: ['API REST', 'Mobile', 'Notificações', 'Documentação'],
    features: [
      'APIs RESTful seguindo padrões REST',
      'Documentação completa com Swagger/OpenAPI',
      'Autenticação JWT com refresh tokens',
      'Sistema de notificações push (FCM)',
      'Cronjobs para automações de negócio',
      'Listeners para eventos do sistema',
      'Versionamento de API',
      'Rate limiting e throttling'
    ],
    challenges: [
      'Desenhar endpoints RESTful intuitivos e consistentes',
      'Implementar autenticação segura com refresh tokens',
      'Garantir performance com grande volume de requisições',
      'Criar documentação que se mantém atualizada',
      'Implementar notificações confiáveis para milhares de usuários',
      'Versionamento sem quebrar apps antigos'
    ],
    metrics: [
      { value: '50+', label: 'Endpoints' },
      { value: '10K+', label: 'Requests/dia' },
      { value: '100%', label: 'Documentado' },
      { value: '<100ms', label: 'Avg Response' }
    ]
  },
  {
    id: 5,
    title: 'Sistema Financeiro proScore',
    role: 'Full Stack Developer',
    shortDescription: 'Desenvolvimento de sistema com complexo cálculo financeiro e APIs com integrações de terceiros.',
    fullDescription: 'Desenvolvimento e otimização de sistema com integrações complexas de APIs externas, implementação de emissão de boletos bancários, lógica de negócio no backend com Laravel e interfaces dinâmicas com jQuery/Ajax e Bootstrap. Aplicação de design patterns para melhorar performance e manutenibilidade.',
    category: 'api',
    icon: 'integration_instructions',
    gradient: 'linear-gradient(135deg, #fbc2eb 0%, #a6c1ee 100%)',
    company: 'ProScore',
    period: '2023',
    type: 'Sistema Completo',
    stack: ['Laravel', 'Silex', 'jQuery', 'Ajax', 'Bootstrap', 'Postgres', 'Redis', 'APIs Terceiros', 'Bitbucket', 'Trello'],
    tags: ['Integrações', 'Pagamentos', 'Refactoring', 'SOLID', 'Performance'],
    features: [
      'Integração completa com APIs de terceiros',
      'Sistema de emissão de boletos bancários',
      'Gestão de vencimentos e validações de pagamento',
      'Aplicação de Service Layer Pattern',
      'Implementação de Repository Pattern',
      'Interface dinâmica com jQuery e Ajax',
      'Layout responsivo com Bootstrap',
      'Uso de Observers para automatização',
      'Implementação de Jobs para processos assíncronos',
      'Otimização de queries com Eager Loading',
      'Cache estratégico com Redis'
    ],
    challenges: [
      'Integrar múltiplas APIs de terceiros com diferentes padrões',
      'Implementar emissão de boletos com diferentes bancos',
      'Refatorar código legado sem quebrar funcionalidades',
      'Criar interfaces dinâmicas sem framework JS moderno',
      'Aplicar patterns sem over-engineering',
      'Melhorar performance mantendo compatibilidade com jQuery',
      'Criar novas regras de cálculo financeiro adicionando-as às que já funcionam',
    ],
    metrics: [
      { value: '60%', label: 'Redução tempo' },
      { value: '5+', label: 'APIs integradas' },
      { value: '3x', label: 'Mais rápido' },
      { value: '100%', label: 'Boletos' }
    ]
  },
  {
    id: 6,
    title: 'Dashboard Claro',
    role: 'Full Stack Developer',
    shortDescription: 'Sistema de gestão e visualização de dados de recuperação com filtros avançados e integrações com sistemas legados.',
    fullDescription: 'Desenvolvimento de dashboard completo para gerenciamento de dados de recuperação extraídos de sistema legado, com funcionalidades de busca avançada, filtros dinâmicos, visualização de dados e integrações automatizadas.',
    category: 'platform',
    icon: 'dashboard',
    gradient: 'linear-gradient(135deg, #ff9a9e 0%, #fecfef 100%)',
    company: 'Claro',
    period: '2024',
    type: 'Dashboard',
    stack: ['Laravel', 'Vue.js', 'MySQL', 'Jobs', 'Quasar'],
    tags: ['Dashboard', 'Data Visualization', 'Filtros', 'Admin'],
    features: [
      'Interface Vue.js com Vuetify responsiva',
      'Sistema de filtros avançados e busca',
      'Visualização de dados em cards e tabelas',
      'Paginação e ordenação server-side',
      'Exportação de dados (CSV, Excel)',
      'Scraping e extração automática de dados',
      'Processamento assíncrono com Jobs',
      'Processamento assíncrono de eventos e comunicação entre serviços usando Apache Kafka',
      'Logs de operações e auditoria',
      'Dashboard com estatísticas'
    ],
    challenges: [
      'Criar filtros dinâmicos performáticos',
      'Lidar com grande volume de registros',
      'Sincronizar dados de múltiplas fontes',
      'Implementar busca eficiente full-text',
      'Criar UX intuitiva para operadores',
      'Otimizar queries com múltiplos joins'
    ],
    metrics: [
      { value: '100K+', label: 'Registros' },
      { value: '80+', label: 'Filtros' },
      { value: '<2s', label: 'Load time' },
      { value: '150+', label: 'Usuários' }
    ]
  }
]

const filteredProjects = computed(() => {
  if (selectedCategory.value === 'all') {
    return projects
  }
  return projects.filter(p => p.category === selectedCategory.value)
})

const getCategoryColor = (category: string) => {
  const colors: Record<string, string> = {
    fiscal: 'purple-7',
    automation: 'pink-7',
    api: 'blue-7',
    platform: 'cyan-7'
  }
  return colors[category] ?? 'grey-7'
}

const getCategoryLabel = (category: string) => {
  const labels: Record<string, string> = {
    fiscal: 'Fiscal',
    automation: 'Automação',
    api: 'API',
    platform: 'Plataforma'
  }
  return labels[category] ?? category
}

const openProjectModal = (project: Project) => {
  selectedProject.value = project
  showModal.value = true
}
</script>

<style scoped lang="scss">
.projects-section {
  padding: 80px 0;
  position: relative;
  background: radial-gradient(circle at 20% 50%, rgba(0, 129, 75, 0.05) 0%, transparent 50%),
  radial-gradient(circle at 80% 80%, rgba(0, 129, 75, 0.05) 0%, transparent 50%);
}

.container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 48px;
}

// Filter buttons
.filter-btn {
  transition: all 0.3s ease;

  &:hover {
    transform: translateY(-2px);
  }
}

// Project cards
.project-card {
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 16px;
  overflow: hidden;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;

  &:hover {
    transform: translateY(-12px);
    border-color: rgba(0, 129, 75, 0.5);
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);

    .project-thumbnail {
      .thumbnail-overlay {
        opacity: 1;
      }
    }

    .card-shine {
      transform: translateX(100%);
    }
  }
}

.project-thumbnail {
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;

  .thumbnail-overlay {
    position: absolute;
    inset: 0;
    background: rgba(0, 0, 0, 0.7);
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transition: opacity 0.3s ease;
  }
}

.card-shine {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
  transform: translateX(-100%);
  transition: transform 0.6s ease;
  pointer-events: none;
}

// Metrics
.metrics-row {
  display: flex;
  gap: 16px;
  padding: 12px;
  background: rgba(0, 129, 75, 0.05);
  border-radius: 8px;
}

.metric-item {
  flex: 1;
  text-align: center;
}

// Modal
.modal-container {
  max-height: 100vh;
  overflow-y: auto;
}

.modal-hero {
  padding: 40px 0;
  position: relative;
  overflow: hidden;

  &::before {
    content: '';
    position: absolute;
    inset: 0;
    background: rgba(0, 0, 0, 0.3);
  }

  .container {
    position: relative;
    z-index: 1;
  }
}

.stack-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

// Responsive
@media (max-width: 1023px) {
  .container {
    padding: 0 24px;
  }

  .projects-section {
    padding: 60px 0;
  }

  .project-thumbnail {
    height: 160px;
  }
}

@media (max-width: 599px) {
  .metrics-row {
    flex-wrap: wrap;
  }

  .metric-item {
    min-width: calc(50% - 8px);
  }

  .filter-btn {
    font-size: 12px;
    padding: 4px 8px;
  }
}
</style>
