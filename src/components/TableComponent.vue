<template>
    <div class="component-table">
        <table v-if="table">
            <thead>
                <tr>
                    <th v-for="(th, i) in table.th" :key="i" v-html="th"></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(row, idx) in table.td" :key="idx">
                    <td v-for="i in Object.keys(row)" :key="i" v-html="formatHtml(row[i])"></td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script setup>
import { ref, onMounted, defineProps } from 'vue'
const props = defineProps({ name: String })
const table = ref(null)

const formatHtml = (text) => text?.replace(/\n/g, '<br>') || ''

onMounted(async () => {
    const res = await fetch('./json/regmed_tables.json')
    const allTables = await res.json()
    table.value = allTables.find(tbl => tbl.title === props.name)
})
</script>
