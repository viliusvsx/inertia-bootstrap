<script setup>

import AppLayout from "@/Layouts/AppLayout.vue";
import Card from "@/Components/Html/Card.vue";
</script>

<template>
    <AppLayout>
        <Card>
            <div class="fw-bold fs-2">
                Welcome,
                <span v-if="$page.props.auth.user">{{ $page.props.auth.user.name}}</span>
                <span v-else>GuestS</span>
            </div>
        </Card>
    </AppLayout>
</template>
