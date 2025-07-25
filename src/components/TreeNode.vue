<template>
    <ul v-if="node">
        <template v-for="(child, i) in node.children || []" :key="i">
            <li>
                <span>
                    <span v-if="level > 0">
                        <span v-if="i === (node.children.length - 1)">└── </span>
                        <span v-else>├── </span>
                    </span>
                    <span class="directory">{{ child.name }}</span>
                    <span v-if="child.note" class="note"> — {{ child.note }}</span>
                </span>
                <div v-if="child.children" style="margin-left: 1.2em;">
                    <TreeNode :node="child" :level="level + 1" />
                </div>
            </li>
        </template>
    </ul>
</template>

<script setup>
const props = defineProps({
    node: Object,
    level: {
        type: Number,
        default: 0
    }
})
</script>

<style scoped>
ul {
    list-style-type: none;
    margin: 0;
    padding-left: 0.2em;
}

.directory {
    color: #58a6ff;
    font-weight: bold;
}

.note {
    color: #8b949e;
    font-style: italic;
}

li {
    white-space: pre;
    font-family: 'Courier New', monospace;
    line-height: 1.2;
}
</style>
