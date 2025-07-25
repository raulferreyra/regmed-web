<template>
    <ul v-if="node">
        <li>
            <span class="directory">{{ node.name }}</span>
            <span v-if="node.note" class="note"> — {{ node.note }}</span>
            <TreeNode v-for="(child, i) in node.children || []" :key="i" :node="child" />
        </li>
    </ul>
</template>

<script setup>
defineProps({ node: Object })
</script>

<style scoped>
ul {
    list-style-type: none;
    margin: 0;
    padding-left: 1em;
}

.directory {
    color: #58a6ff;
    font-weight: bold;
}

.note {
    color: #8b949e;
    font-style: italic;
}
</style>
