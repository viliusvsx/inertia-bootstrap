<script setup>
import { useForm } from '@inertiajs/vue3';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import Modal from '@/Components/Modal.vue';
import TextInput from '@/Components/TextInput.vue';
import {nextTick, onMounted, reactive, ref} from 'vue';

onMounted(() => {
    state.modalDemo = new bootstrap.Modal('#deleteModal', {})
})

const state = reactive({
    modalDemo: null,
})

const passwordInput = ref(null);

const form = useForm({
    password: '',
});

const confirmUserDeletion = () => {
    state.modalDemo.show();
    nextTick(() => passwordInput.value.focus());
};

const deleteUser = () => {
    form.delete(route('profile.destroy'), {
        preserveScroll: true,
        onSuccess: () => closeModal(),
        onError: () => passwordInput.value.focus(),
        onFinish: () => form.reset(),
    });
};

const closeModal = () => {
    state.modalDemo.hide();
    form.reset();
    setTimeout(() => {
        form.clearErrors();
    }, 200)
};
</script>

<template>
    <section>
        <header>
            <h2>Delete Account</h2>
            <p>
                Once your account is deleted, all of its resources and data will be permanently deleted. Before deleting
                your account, please download any data or information that you wish to retain.
            </p>
        </header>

        <button class="btn btn-danger" type="submit" @click="confirmUserDeletion">Delete Account</button>

        <Modal name="deleteModal" @close="closeModal">
            <div class="p-1">
                <h2>
                    Are you sure you want to delete your account?
                </h2>

                <p>
                    Once your account is deleted, all of its resources and data will be permanently deleted. Please
                    enter your password to confirm you would like to permanently delete your account.
                </p>

                <div class="mt-3">
                    <InputLabel for="password" value="Password" />

                    <TextInput
                        id="password"
                        ref="passwordInput"
                        v-model="form.password"
                        type="password"
                        placeholder="Password"
                        @keyup.enter="deleteUser"
                    />

                    <InputError :message="form.errors.password" />
                </div>
            </div>

            <template #modalFooter>
                <div class="d-flex justify-content-end gap-1 p-3">
                    <button class="btn btn-secondary" type="button" @click="closeModal"> Cancel </button>

                    <button
                        class="btn btn-danger"
                        type="button"
                        :disabled="form.processing"
                        @click="deleteUser"
                    >
                        Delete Account
                    </button>
                </div>
            </template>
        </Modal>
    </section>
</template>
