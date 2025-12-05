<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated class="bg-dark text-white">
      <q-toolbar class="q-px-xl">
        <q-toolbar-title class="text-weight-bold">
          Diego Rodrigues
        </q-toolbar-title>

        <div class="row items-center q-gutter-sm gt-sm">
          <q-btn flat label="Início" @click="scrollTo('hero')" />
          <q-btn flat label="Sobre" @click="scrollTo('about')" />
          <q-btn flat label="Experiência" @click="scrollTo('experience')" />
          <q-btn flat label="Projetos" @click="scrollTo('projects')" />
          <q-btn flat label="Skills" @click="scrollTo('skills')" />
          <q-btn flat label="Contato" @click="scrollTo('contact')" />
        </div>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <q-page padding class="bg-grey-10 text-grey-1">
        <HeroSection id="hero" />
        <AboutSection id="about" class="q-mt-xl" />
        <ExperienceSection id="experience" class="q-mt-xl" />
        <ProjectsSection id="projects" class="q-mt-xl" />
        <SkillsSection id="skills" class="q-mt-xl" />
        <ContactSection id="contact" class="q-mt-xl q-mb-xl" />
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<script setup lang="ts">
import { scroll } from 'quasar'
import HeroSection from 'src/components/HeroSection.vue'
import AboutSection from 'src/components/AboutSection.vue'
import ExperienceSection from 'src/components/ExperienceSection.vue'
import ProjectsSection from 'src/components/ProjectsSection.vue'
import SkillsSection from 'src/components/SkillsSection.vue'
import ContactSection from 'src/components/ContactSection.vue'

const { setVerticalScrollPosition } = scroll

const scrollTo = (targetId: string) => {
  const el = document.getElementById(targetId)
  if (!el) return

  const pageOffset = el.offsetTop - 70 // descontar header
  setVerticalScrollPosition(window, pageOffset, 400)
}
</script>
