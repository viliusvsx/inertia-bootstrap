<script setup>
defineProps(['value']);
</script>

<template>
    <label class="form-label m-0">
        <span v-if="value">{{ value }}</span>
        <span v-else><slot /></span>
    </label>
</template>
