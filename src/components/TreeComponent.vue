<template>
    <div class="component-tree">
        <TreeNode :node="treeData" />
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
const treeData = ref({})

onMounted(async () => {
    const res = await fetch('/json/tree.json')
    treeData.value = await res.json()
})

const TreeNode = {
    props: ['node'],
    template: `
    <ul>
      <li>
        <span class="directory">{{ node.name }}</span>
        <span v-if="node.note" class="note"> — {{ node.note }}</span>
        <TreeNode
          v-for="(child, i) in node.children || []"
          :key="i"
          :node="child"
        />
      </li>
    </ul>
  `,
    components: { TreeNode: null }
}
TreeNode.components.TreeNode = TreeNode
</script>
