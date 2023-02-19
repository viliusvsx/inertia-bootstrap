<script setup>
defineProps(['message']);
</script>

<template>
    <div v-show="message">
        <p class="text-danger fw-bold">
            {{ message }}
        </p>
    </div>
</template>
