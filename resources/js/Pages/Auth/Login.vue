<script setup>
import {Head, Link, useForm} from '@inertiajs/vue3';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import TextInput from '@/Components/TextInput.vue';
import AppLayout from "@/Layouts/AppLayout.vue";
import Card from "@/Components/Html/Card.vue";

defineProps({
    canResetPassword: Boolean,
    status: String,
});

const form = useForm({
    email: '',
    password: '',
    remember: false,
});

const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
</script>

<template>
    <AppLayout>
        <Head title="Log in"/>

        <Card>
            <form @submit.prevent="submit">
                <div>
                    <InputLabel for="email" value="Email"/>

                    <TextInput
                        id="email"
                        type="email"
                        v-model="form.email"
                        required
                        autofocus
                        autocomplete="username"
                    />

                    <InputError :message="form.errors.email"/>
                </div>

                <div class="mt-4">
                    <InputLabel for="password" value="Password"/>

                    <TextInput
                        id="password"
                        type="password"
                        v-model="form.password"
                        required
                        autocomplete="current-password"
                    />

                    <InputError :message="form.errors.password"/>
                </div>

                <div class="mt-4">
                    <label class="d-flex">
                        <input class="form-check-input" type="checkbox" name="remember" v-model="form.remember"/>
                        <span class="ms-1">Remember me</span>
                    </label>
                </div>

                <div class="d-flex justify-content-center align-items-center gap-3">
                    <Link
                        v-if="canResetPassword"
                        :href="route('password.request')"
                        class="fw-bold text-decoration-none"
                    >
                        Forgot your password?
                    </Link>

                    <button class="btn btn-primary" type="submit" :disabled="form.processing">
                        Log in
                    </button>
                </div>
            </form>
        </Card>
    </AppLayout>
</template>
