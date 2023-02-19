<script setup>
import { Head } from '@inertiajs/vue3';
import AppLayout from '@/Layouts/AppLayout.vue';
import Card from "@/Components/Html/Card.vue";
</script>

<template>
    <Head title="Dashboard" />

    <AppLayout>
        <Card>
            You're logged in!
        </Card>
    </AppLayout>
</template>
