<script setup>
import AppLayout from "@/Layouts/AppLayout.vue";
import Card from "@/Components/Html/Card.vue";
import {Head} from "@inertiajs/vue3";
</script>

<template>
    <AppLayout>
        <Head title="Welcome"/>

        <Card>
            <div class="fw-bold fs-2">
                Welcome,
                <span v-if="$page.props.auth.user">{{ $page.props.auth.user.name}}</span>
                <span v-else>Guest</span>
            </div>
        </Card>
    </AppLayout>
</template>
