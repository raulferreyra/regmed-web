<template>
  <section class="main" v-for="(section, index) in sections" :key="index">
    <article>
      <div class="content">
        <h1 v-if="section.title">{{ section.title }}</h1>
        <h2 v-if="section.subtitle">{{ section.subtitle }}</h2>
        <p v-if="section.content" v-html="section.content"></p>
      </div>
      <img v-if="section.image" :src="section.image" alt="" />
    </article>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const sections = ref([])

onMounted(async () => {
  try {
    const res = await fetch('./json/regmed_principal_content.json')
    if (!res.ok) throw new Error('No se pudo cargar el JSON.')
    sections.value = await res.json()
  } catch (err) {
    console.error('Error cargando JSON:', err)
  }
})
</script>