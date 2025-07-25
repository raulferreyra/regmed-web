<template>
  <div class="component-tree" v-if="treeData">
    <TreeNode :node="treeData" />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import TreeNode from './TreeNode.vue'

const treeData = ref(null)

onMounted(async () => {
  const res = await fetch('./json/regmed_project_tree.json')
  treeData.value = await res.json()
})
</script>

<style scoped>
.component-tree {
  background: #0d1117;
  color: #c9d1d9;
  padding: 1.5rem;
  border-radius: 10px;
  font-family: 'Courier New', monospace;
}
</style>
