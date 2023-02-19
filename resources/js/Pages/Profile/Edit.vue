<script setup>
import {Head} from '@inertiajs/vue3';
import AppLayout from '@/Layouts/AppLayout.vue';
import DeleteUserForm from './Partials/DeleteUserForm.vue';
import UpdatePasswordForm from './Partials/UpdatePasswordForm.vue';
import UpdateProfileInformationForm from './Partials/UpdateProfileInformationForm.vue';

defineProps({
    mustVerifyEmail: Boolean,
    status: String,
});
</script>

<template>
    <Head title="Profile" />

    <AppLayout>
        <div class="container">
            <div class="py-4">
                <div class="d-flex flex-column gap-3">
                    <div class="bg-white p-4 rounded-5 border border-2">
                        <UpdateProfileInformationForm
                            :must-verify-email="mustVerifyEmail"
                            :status="status"
                            class="col-12"
                        />
                    </div>

                    <div class="bg-white p-4 rounded-5 border border-2">
                        <UpdatePasswordForm class="col-12" />
                    </div>

                    <div class="bg-white p-4 rounded-5 border border-2">
                        <DeleteUserForm class="col-12" />
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
