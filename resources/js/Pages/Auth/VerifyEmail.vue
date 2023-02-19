<script setup>
import { Head, Link, useForm } from '@inertiajs/vue3';
import { computed } from 'vue';
import AppLayout from "@/Layouts/AppLayout.vue";
import Card from "@/Components/Html/Card.vue";

const props = defineProps({
    status: String,
});

const form = useForm({});

const submit = () => {
    form.post(route('verification.send'));
};

const verificationLinkSent = computed(() => props.status === 'verification-link-sent');
</script>

<template>
    <AppLayout>
        <Head title="Email Verification" />

        <Card>
            <div class="mb-3">
                Thanks for signing up! Before getting started, could you verify your email address by clicking on the link
                we just emailed to you? If you didn't receive the email, we will gladly send you another.
            </div>

            <div class="mb-3" v-if="verificationLinkSent">
                A new verification link has been sent to the email address you provided during registration.
            </div>

            <form @submit.prevent="submit">
                <div class="d-flex justify-content-between align-items-center mt-3">
                    <button class="btn btn-primary" type="submit" :disabled="form.processing">
                        Resend Verification Email
                    </button>

                    <Link
                        :href="route('logout')"
                        method="post"
                        as="button"
                        class="btn btn-secondary"
                    >Log Out</Link>
                </div>
            </form>
        </Card>
    </AppLayout>
</template>
