<template>
    <section v-for="(block, index) in content" :key="index" :class="block.style_non ? 'component-non' : 'component'">
        <article>
            <h2 v-if="block.title">{{ block.title }}</h2>
            <p v-if="block.content" v-html="formatHtml(block.content)"></p>

            <img v-if="block.image" :src="block.image" alt="" />
        </article>
    </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const content = ref([])
const formatHtml = (text) => {
    return text?.replace(/\n/g, '<br/>') || ''
}

onMounted(async () => {
    try {
        const res = await fetch('./json/regmed_page_content.json')
        if (!res.ok) throw new Error('No se pudo cargar el JSON')
        content.value = await res.json()
    } catch (err) {
        console.error('Error cargando regmed_page_content.json:', err)
    }
})
</script>