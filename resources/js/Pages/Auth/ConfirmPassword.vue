<script setup>
import { Head, useForm } from '@inertiajs/vue3';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import TextInput from '@/Components/TextInput.vue';
import AppLayout from "@/Layouts/AppLayout.vue";
import Card from "@/Components/Html/Card.vue";

const form = useForm({
    password: '',
});

const submit = () => {
    form.post(route('password.confirm'), {
        onFinish: () => form.reset(),
    });
};
</script>

<template>
    <AppLayout>
        <Head title="Confirm Password" />

        <Card>
            <div class="mb-3">
                This is a secure area of the application. Please confirm your password before continuing.
            </div>

            <form @submit.prevent="submit">
                <div>
                    <InputLabel for="password" value="Password" />
                    <TextInput
                        id="password"
                        type="password"
                        v-model="form.password"
                        required
                        autocomplete="current-password"
                        autofocus
                    />
                    <InputError class="mt-1" :message="form.errors.password" />
                </div>

                <div class="d-flex mt-3">
                    <button class="btn btn-primary" type="submit" :disabled="form.processing">
                        Confirm
                    </button>
                </div>
            </form>
        </Card>
    </AppLayout>
</template>
