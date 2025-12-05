<template>
  <section :id="id" class="experience-section">
    <div class="container">
      <!-- Section Header -->
      <div class="text-center q-mb-xl" data-aos="fade-up">
        <div class="text-overline text-primary text-weight-bold">Trajetória</div>
        <h2 class="text-h3 text-weight-bold q-mb-sm">Experiência Profissional</h2>
        <p class="text-body1 text-grey-4" style="max-width: 600px; margin: 0 auto;">
          +3 anos construindo soluções em diferentes segmentos e desafios
        </p>
      </div>

      <!-- Timeline -->
      <q-timeline color="primary" layout="comfortable" class="custom-timeline">
        <q-timeline-entry
          v-for="(job, index) in jobs"
          :key="index"
          :title="job.title"
          :subtitle="job.company"
          :icon="job.icon"
          :color="job.color"
          data-aos="fade-up"
          :data-aos-delay="index * 100"
        >
          <template v-slot:subtitle>
            <div class="row items-center q-gutter-sm">
              <div class="text-weight-bold">{{ job.company }}</div>
              <q-separator vertical />
              <div class="text-caption">{{ job.period }}</div>
              <q-badge
                v-if="job.current"
                color="positive"
                label="Atual"
                class="q-ml-xs"
              />
            </div>
          </template>

          <q-card
            flat
            class="experience-card bg-grey-9"
            :class="{ 'expanded': expandedCards[index] }"
          >
            <q-card-section>
              <!-- Description -->
              <div class="text-body2 text-grey-3 q-mb-md" style="line-height: 1.7;">
                {{ job.description }}
              </div>

              <!-- Key achievements (visible in expanded mode) -->
              <div v-if="expandedCards[index] && job.achievements.length > 0" class="q-mb-md">
                <div class="text-subtitle2 text-weight-bold q-mb-sm">
                  <q-icon name="emoji_events" size="18px" class="q-mr-xs text-primary" />
                  Principais Conquistas
                </div>
                <q-list dense class="achievements-list">
                  <q-item
                    v-for="(achievement, idx) in job.achievements"
                    :key="idx"
                    class="q-px-none"
                  >
                    <q-item-section avatar style="min-width: 30px;">
                      <q-icon name="check_circle" size="16px" class="text-positive" />
                    </q-item-section>
                    <q-item-section>
                      <q-item-label class="text-body2 text-grey-3">
                        {{ achievement }}
                      </q-item-label>
                    </q-item-section>
                  </q-item>
                </q-list>
              </div>

              <!-- Technologies -->
              <div class="q-mb-sm">
                <div class="text-caption text-grey-5 q-mb-xs">Tecnologias utilizadas</div>
                <div class="row q-gutter-xs">
                  <q-chip
                    v-for="tech in job.technologies"
                    :key="tech.name"
                    dense
                    :color="tech.color"
                    text-color="white"
                    size="sm"
                    class="tech-chip"
                  >
                    <q-icon
                      v-if="tech.icon"
                      :name="tech.icon"
                      size="14px"
                      class="q-mr-xs"
                    />
                    {{ tech.name }}
                  </q-chip>
                </div>
              </div>

              <!-- Expand/Collapse button -->
              <div class="text-center q-mt-md" v-if="job.achievements.length > 0">
                <q-btn
                  flat
                  dense
                  size="sm"
                  :label="expandedCards[index] ? 'Ver menos' : 'Ver mais detalhes'"
                  :icon-right="expandedCards[index] ? 'expand_less' : 'expand_more'"
                  color="primary"
                  @click="toggleCard(index)"
                />
              </div>
            </q-card-section>
          </q-card>
        </q-timeline-entry>
      </q-timeline>

      <!-- Skills acquired section -->
      <div class="skills-acquired q-mt-xl" data-aos="fade-up">
        <q-card flat class="bg-grey-9">
          <q-card-section class="q-pa-lg">
            <div class="row items-center q-mb-md">
              <q-icon name="school" size="32px" class="text-primary q-mr-sm" />
              <div class="text-h6 text-weight-bold">Habilidades Desenvolvidas</div>
            </div>

            <div class="row q-col-gutter-md">
              <div class="col-12 col-md-4">
                <div class="skill-category">
                  <div class="text-subtitle2 text-primary q-mb-sm">
                    <q-icon name="code" class="q-mr-xs" />
                    Técnicas
                  </div>
                  <q-list dense>
                    <q-item v-for="skill in technicalSkills" :key="skill" class="q-px-none">
                      <q-item-section avatar style="min-width: 30px;">
                        <q-icon name="arrow_right" size="16px" class="text-primary" />
                      </q-item-section>
                      <q-item-section>
                        <q-item-label class="text-body2">{{ skill }}</q-item-label>
                      </q-item-section>
                    </q-item>
                  </q-list>
                </div>
              </div>

              <div class="col-12 col-md-4">
                <div class="skill-category">
                  <div class="text-subtitle2 text-green-7 q-mb-sm">
                    <q-icon name="groups" class="q-mr-xs" />
                    Soft Skills
                  </div>
                  <q-list dense>
                    <q-item v-for="skill in softSkills" :key="skill" class="q-px-none">
                      <q-item-section avatar style="min-width: 30px;">
                        <q-icon name="arrow_right" size="16px" class="text-green-7" />
                      </q-item-section>
                      <q-item-section>
                        <q-item-label class="text-body2">{{ skill }}</q-item-label>
                      </q-item-section>
                    </q-item>
                  </q-list>
                </div>
              </div>

              <div class="col-12 col-md-4">
                <div class="skill-category">
                  <div class="text-subtitle2 text-blue-7 q-mb-sm">
                    <q-icon name="business_center" class="q-mr-xs" />
                    Domínios
                  </div>
                  <q-list dense>
                    <q-item v-for="skill in domainSkills" :key="skill" class="q-px-none">
                      <q-item-section avatar style="min-width: 30px;">
                        <q-icon name="arrow_right" size="16px" class="text-blue-7" />
                      </q-item-section>
                      <q-item-section>
                        <q-item-label class="text-body2">{{ skill }}</q-item-label>
                      </q-item-section>
                    </q-item>
                  </q-list>
                </div>
              </div>
            </div>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

defineProps({
  id: {
    type: String,
    default: 'experience'
  }
})

const expandedCards = ref<Record<number, boolean>>({})

const toggleCard = (index: number) => {
  expandedCards.value[index] = !expandedCards.value[index]
}

const jobs = [
  {
    title: 'Desenvolvedor Full Stack',
    company: 'Claro',
    period: '2025',
    current: true,
    icon: 'code',
    color: 'red-8',
    description: 'Desenvolvimento e modernização do sistema legado de incidentes, com foco em automações, web scraping e processamento assíncrono de grandes volumes de dados regulatórios de telecomunicações.',
    achievements: [
      'Desenvolvi sistema de web scraping robusto para extração automática de dados de sistema legado, com tratamento inteligente de sessões e timeouts',
      'Implementei arquitetura de jobs em fila (Laravel Queues + Redis) para processamento assíncrono de até 10.000+ registros simultâneos',
      'Criei sistema de gerenciamento de sessões com auto-renovação e tratamento de expiração, reduzindo falhas em 95%',
      'Implementei dashboard em Vue.js com tabelas dinâmicas, paginação server-side, filtros avançados e gráficos ApexCharts para visualização de dados regulatórios',
      'Desenvolvi sistema de logs estruturados e monitoramento em tempo real de processos críticos com alertas automáticos',
      'Otimizei queries MySQL complexas, reduzindo tempo de processamento de relatórios de 5min para 30s',
    ],
    technologies: [
      { name: 'Laravel 7', color: 'red-8', icon: null },
      { name: 'Vue.js 3', color: 'green-7', icon: null },
      { name: 'PHP 7.4', color: 'purple-7', icon: null },
      { name: 'Redis/Queues', color: 'red-7', icon: null },
      { name: 'Web Scraping', color: 'grey-7', icon: null },
      { name: 'MySQL', color: 'blue-8', icon: null },
      { name: 'ApexCharts', color: 'orange-7', icon: null },
      { name: 'Composer', color: 'yellow-9', icon: null },
    ]
  },
  {
    title: 'Full Stack Developer',
    company: 'Attimo Soluções',
    period: '2024 - 2025',
    current: false,
    icon: 'work',
    color: 'primary',
    description: 'Desenvolvimento e manutenção de sistemas fiscais complexos com Laravel + Vue.js. Implementação de emissão de NFe/NFC-e com integrações SEFAZ, gerenciamento de certificados digitais, multi-tenancy e painéis administrativos robustos.',
    achievements: [
      'Implementei sistema completo de emissão de NFe/NFC-e com integrações SEFAZ para múltiplos estados',
      'Desenvolvi arquitetura multi-empresa com isolamento de dados e gestão de contexto',
      'Criei sistema de importação automática de produtos com validações e tratamento de erros',
      'Implementei gestão de certificados digitais A1 e A3 com renovação automática',
      'Otimizei queries complexas reduzindo tempo de resposta em 60%'
    ],
    technologies: [
      { name: 'Laravel', color: 'red-8', icon: null },
      { name: 'Vue.js', color: 'green-7', icon: null },
      { name: 'Filament', color: 'orange-7', icon: null },
      { name: 'PostgreSQL', color: 'blue-7', icon: null },
      { name: 'Redis', color: 'red-7', icon: null },
      { name: 'Docker', color: 'blue-6', icon: null }
    ]
  },
  {
    title: 'Líder Técnico',
    company: 'BetSolve',
    period: '2025',
    current: false,
    icon: 'sports_esports',
    color: 'green-7',
    description: 'Liderança técnica no desenvolvimento de plataforma de apostas esportivas e jogos online . Coordenação de equipe, implementação de sistemas transacionais com alto volume, processamento de pagamentos e gestão de prêmios.',
    achievements: [
      'Liderei equipe de 3 desenvolvedores coordenando sprints e entregas',
      'Implementei integração completa com gateways de pagamento (webhooks, callbacks)',
      'Desenvolvi sistema de gestão de prêmios e saques com auditoria completa',
      'Criei arquitetura para jogos digitais com alta disponibilidade',
      'Implementei boas práticas de segurança seguindo diretrizes OWASP'
    ],
    technologies: [
      { name: 'Laravel 11', color: 'red-8', icon: null },
      { name: 'Lúmen', color: 'red-6', icon: null },
      { name: 'PHP 8.2', color: 'purple-7', icon: null },
      { name: 'Alpine', color: 'orange-6', icon: null },
      { name: 'React', color: 'blue-8', icon: null },
      { name: 'Vue.js', color: 'green-7', icon: null },
      { name: 'MySql', color: 'blue-7', icon: null },
      { name: 'Redis', color: 'red-7', icon: null },
      { name: 'Payment APIs', color: 'green-8', icon: null }
    ]
  },
  {
    title: 'Desenvolvedor Backend',
    company: 'Grupo Águia',
    period: 'Out/2023 - Ago/2024',
    current: false,
    icon: 'api',
    color: 'blue-7',
    description: 'Desenvolvimento backend para aplicativos mobile com Laravel. Criação de APIs REST documentadas com Swagger, implementação de cronjobs, listeners para automação e sistema de notificações em tempo real. Trabalho em sprints ágeis com foco em qualidade.',
    achievements: [
      'Desenvolvi APIs REST completas documentadas com Swagger/OpenAPI',
      'Implementei sistema de notificações push em tempo real',
      'Criei cronjobs e listeners para automação de processos de negócio',
      'Implementei autenticação JWT com refresh tokens',
      'Participei ativamente de code reviews e pair programming'
    ],
    technologies: [
      { name: 'Laravel', color: 'red-8', icon: null },
      { name: 'APIs REST', color: 'blue-7', icon: null },
      { name: 'Swagger', color: 'green-8', icon: null },
      { name: 'MySQL', color: 'blue-8', icon: null },
      { name: 'JWT', color: 'purple-7', icon: null },
      { name: 'JIRA', color: 'blue-6', icon: null },
      { name: 'Payment APIs', color: 'green-8', icon: null }
    ]
  },
  {
    title: 'Desenvolvedor Full Stack',
    company: 'ProScore',
    period: 'Ago/2024 - Set/2025',
    current: false,
    icon: 'speed',
    color: 'orange-7',
    description: 'Desenvolvimento e otimização de APIs com integrações de terceiros, emissão de boletos, ' +
      'lógica complexa no backend (cálculos financeiros) e frontend com jQuery/Ajax. Aplicação de design patterns ' +
      '(Services, Repositories, Observers, Jobs e index no banco) para melhorar performance e manutenibilidade.',
    achievements: [
      'Implementei integração com Pagarme, Neurotech, Sendgrid e outras APIs de terceiros',
      'Utilizei API do Banco do Brasil para emissão de boletos com validações e gestão de vencimentos',
      'Criei e mantive lógica complexa de negócio no backend com Laravel: ' +
      'Cálculo de juros, parcelas e lógica para financiamento de veículos',
      'Automatizei funcionalidades para facilitar o uso do sistema: ' +
      'Validação de regras personalizadas para aprovação ou recusa de crédito',
      'Criei regras de acesso com tabela pivot para restringir usuários não permitidos',
      'Desenvolvi interfaces dinâmicas com jQuery, Ajax e Bootstrap',
      'Apliquei design patterns reduzindo significativamente tempo de resposta das APIs',
      'Refatorei código legado seguindo princípios SOLID'
    ],
    technologies: [
      { name: 'Laravel', color: 'red-8', icon: null },
      { name: 'jQuery', color: 'blue-7', icon: null },
      { name: 'Ajax', color: 'orange-7', icon: null },
      { name: 'Bootstrap', color: 'purple-7', icon: null },
      { name: 'APIs Terceiros', color: 'green-7', icon: null },
      { name: 'MySQL', color: 'blue-8', icon: null },
      { name: 'Redis', color: 'red-7', icon: null },
      { name: 'Bitbucket', color: 'blue-4', icon: null },
    ]
  },
  {
    title: 'Desenvolvedor Full Stack',
    company: 'Tevah Solutions',
    period: '2020 - Atual',
    current: true,
    icon: 'business',
    color: 'primary',
    description: 'Negócio próprio desenvolvendo projetos web sob demanda. Criação de aplicações personalizadas, integrações com meios de pagamento, automação de processos internos e desenvolvimento de sistemas para clientes de pequeno e médio porte.',
    achievements: [
      'Desenvolvi 20+ projetos para diferentes clientes e segmentos',
      'Criei integrações com diversos gateways de pagamento',
      'Implementei automações que reduziram trabalho manual em até 80%',
      'Mantive taxa de satisfação de clientes acima de 95%'
    ],
    technologies: [
      { name: 'Laravel', color: 'red-8', icon: null },
      { name: 'Vue.js', color: 'green-7', icon: null },
      { name: 'Quasar', color: 'blue-7', icon: null },
      { name: 'PostgreSQL', color: 'blue-7', icon: null },
      { name: 'Docker', color: 'blue-6', icon: null },
      { name: 'Payment APIs', color: 'green-8', icon: null },
    ]
  }
]

const technicalSkills = [
  'Arquitetura de sistemas complexos',
  'Design Patterns (SOLID, Repository, Service)',
  'APIs RESTful e integrações',
  'Filas e processamento assíncrono',
  'Otimização de queries e performance',
  'Testes automatizados'
]

const softSkills = [
  'Liderança técnica de equipes',
  'Metodologias ágeis (SCRUM)',
  'Comunicação com stakeholders',
  'Trabalho remoto autônomo',
  'Resolução de problemas complexos',
  'Code review e mentoria'
]

const domainSkills = [
  'Sistemas fiscais',
  'Plataformas transacionais',
  'E-commerce e pagamentos',
  'Automação e web scraping',
  'Dashboards e relatórios',
  'Multi-tenancy'
]
</script>

<style scoped lang="scss">
.experience-section {
  padding: 80px 0;
  background: linear-gradient(180deg, transparent 0%, rgba(0, 129, 75, 0.02) 50%, transparent 100%);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 48px;
}

// Custom timeline
.custom-timeline {
  :deep(.q-timeline__subtitle) {
    opacity: 1;
  }

  :deep(.q-timeline__dot) {
    &:before {
      animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
    }
  }
}

@keyframes pulse {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0.5;
  }
}

// Experience cards
.experience-card {
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  transition: all 0.3s ease;
  overflow: hidden;

  &:hover {
    border-color: rgba(0, 129, 75, 0.3);
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.3);
    transform: translateX(8px);
  }

  &.expanded {
    border-color: rgba(0, 129, 75, 0.4);
  }
}

// Achievements list
.achievements-list {
  background: rgba(0, 129, 75, 0.05);
  border-radius: 8px;
  padding: 12px;
}

// Tech chips
.tech-chip {
  transition: all 0.3s ease;

  &:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
  }
}

// Skills acquired section
.skills-acquired {
  :deep(.q-card) {
    border: 1px solid rgba(255, 255, 255, 0.1);
    transition: all 0.3s ease;

    &:hover {
      border-color: rgba(0, 129, 75, 0.3);
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
    }
  }
}

.skill-category {
  padding: 16px;
  background: rgba(255, 255, 255, 0.02);
  border-radius: 8px;
  height: 100%;
}

// Responsive
@media (max-width: 1023px) {
  .container {
    padding: 0 24px;
  }

  .experience-section {
    padding: 60px 0;
  }

  .experience-card {
    &:hover {
      transform: translateX(0) translateY(-4px);
    }
  }
}

@media (max-width: 599px) {
  :deep(.q-timeline) {
    padding-left: 24px;
  }
}
</style>
