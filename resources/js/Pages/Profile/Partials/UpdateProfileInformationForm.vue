<script setup>
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import TextInput from '@/Components/TextInput.vue';
import { Link, useForm, usePage } from '@inertiajs/vue3';

const props = defineProps({
    mustVerifyEmail: Boolean,
    status: String,
});

const user = usePage().props.auth.user;

const form = useForm({
    name: user.name,
    email: user.email,
});
</script>

<template>
    <section>
        <header>
            <h2>Profile Information</h2>
            <p>Update your account's profile information and email address.</p>
        </header>

        <form @submit.prevent="form.patch(route('profile.update'))">
            <div class="mt-3">
                <InputLabel for="name" value="Name" />

                <TextInput
                    id="name"
                    type="text"
                    v-model="form.name"
                    autofocus
                    autocomplete="name"
                />

                <InputError :message="form.errors.name" />
            </div>

            <div class="mt-3">
                <InputLabel for="email" value="Email" />

                <TextInput
                    id="email"
                    type="email"
                    v-model="form.email"
                    autocomplete="username"
                />

                <InputError :message="form.errors.email" />
            </div>

            <div v-if="props.mustVerifyEmail && user.email_verified_at === null">
                <p>
                    Your email address is unverified.
                    <Link
                        :href="route('verification.send')"
                        method="post"
                        as="button"
                        class="btn btn-secondary"
                    >
                        Click here to re-send the verification email.
                    </Link>
                </p>

                <div
                    v-show="props.status === 'verification-link-sent'"
                    class="text-success fw-bold"
                >
                    A new verification link has been sent to your email address.
                </div>
            </div>

            <div class="d-flex align-items-center gap-3 mt-3">
                <button class="btn btn-primary" type="submit" :disabled="form.processing">Save</button>

                <Transition>
                    <p v-if="form.recentlySuccessful" class="fw-bold m-0 text-success">Saved.</p>
                </Transition>
            </div>
        </form>
    </section>
</template>
