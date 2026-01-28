<template>
  <section :id="id" class="contact-section">
    <div class="container">
      <!-- Section Header -->
      <div class="text-center q-mb-xl" data-aos="fade-up">
        <div class="text-h5 text-primary text-weight-bold">Entre em contato</div>
        <h2 class="text-h3 text-weight-bold q-mb-sm">Vamos conversar?</h2>
        <p class="text-body1 text-grey-4" style="max-width: 600px; margin: 0 auto;">
          Está buscando alguém para evoluir um sistema ou tirar um projeto do papel?
        </p>
      </div>

      <!-- Contact methods - Centered -->
      <div class="row justify-center">
        <div class="col-12 col-md-8 col-lg-6" data-aos="fade-up">
          <q-card flat class="contact-card bg-grey-9">
            <q-card-section class="q-pa-lg">
              <div class="text-h6 text-weight-bold q-mb-md text-center">
                <q-icon name="contacts" class="q-mr-sm text-primary" />
                Informações de Contato
              </div>

              <q-list>
                <q-item
                  clickable
                  tag="a"
                  :href="`mailto:${email}`"
                  class="contact-item"
                >
                  <q-item-section avatar>
                    <q-avatar color="red-7" text-color="white">
                      <q-icon name="mail" />
                    </q-avatar>
                  </q-item-section>
                  <q-item-section>
                    <q-item-label class="text-weight-medium">{{ email }}</q-item-label>
                  </q-item-section>
                  <q-item-section side>
                    <q-icon name="arrow_forward" color="grey-5" />
                  </q-item-section>
                </q-item>

                <q-item
                  clickable
                  tag="a"
                  :href="whatsapp"
                  target="_blank"
                  class="contact-item"
                >
                  <q-item-section avatar>
                    <q-avatar color="green-7" text-color="white">
                      <q-icon name="mdi-whatsapp" />
                    </q-avatar>
                  </q-item-section>
                  <q-item-section>
                    <q-item-label class="text-weight-medium">WhatsApp</q-item-label>
                  </q-item-section>
                  <q-item-section side>
                    <q-icon name="arrow_forward" color="grey-5" />
                  </q-item-section>
                </q-item>

                <q-item
                  clickable
                  tag="a"
                  :href="linkedin"
                  target="_blank"
                  class="contact-item"
                >
                  <q-item-section avatar>
                    <q-avatar color="blue-7" text-color="white">
                      <q-icon name="mdi-linkedin" />
                    </q-avatar>
                  </q-item-section>
                  <q-item-section>
                    <q-item-label class="text-weight-medium">LinkedIn</q-item-label>
                  </q-item-section>
                  <q-item-section side>
                    <q-icon name="arrow_forward" color="grey-5" />
                  </q-item-section>
                </q-item>

                <q-item
                  clickable
                  tag="a"
                  :href="github"
                  target="_blank"
                  class="contact-item"
                >
                  <q-item-section avatar>
                    <q-avatar color="grey-8" text-color="white">
                      <q-icon name="mdi-github" />
                    </q-avatar>
                  </q-item-section>
                  <q-item-section>
                    <q-item-label class="text-weight-medium">GitHub</q-item-label>
                  </q-item-section>
                  <q-item-section side>
                    <q-icon name="arrow_forward" color="grey-5" />
                  </q-item-section>
                </q-item>
              </q-list>
            </q-card-section>
          </q-card>
        </div>
      </div>

    </div>
  </section>
</template>

<script setup lang="ts">
defineProps({
  id: {
    type: String,
    default: 'contact'
  }
})

const email = 'diego.devwebb@gmail.com'
const whatsapp = 'https://wa.me/5511940777582' // Substitua pelo seu número
const linkedin = 'https://www.linkedin.com/in/diego-rodrigues-500b0081/'
const github = 'https://github.com/diegodevweb'
</script>

<style scoped lang="scss">
.contact-section {
  padding: 80px 0;
  background: linear-gradient(180deg, transparent 0%, rgba(0, 129, 75, 0.03) 100%);
}

.container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 48px;
}


// Contact cards
.contact-card {
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 16px;
  transition: all 0.3s ease;

  &:hover {
    transform: translateY(-4px);
    border-color: rgba(0, 129, 75, 0.3);
    box-shadow: 0 12px 24px rgba(0, 0, 0, 0.3);
  }
}

.contact-item {
  padding: 16px;
  margin-bottom: 8px;
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.02);
  transition: all 0.3s ease;

  &:hover {
    background: rgba(0, 129, 75, 0.1);
    transform: translateX(8px);

    .q-item__section--side {
      transform: translateX(4px);
    }
  }
}

// Responsive
@media (max-width: 1023px) {
  .container {
    padding: 0 24px;
  }

  .contact-section {
    padding: 60px 0;
  }
}

@media (max-width: 599px) {
  .contact-item {
    &:hover {
      transform: translateX(0) translateY(-2px);
    }
  }
}
</style>
