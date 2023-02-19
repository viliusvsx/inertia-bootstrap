<script setup>
const props = defineProps({
    name: {
        type: String,
    },
    closeable: {
        type: Boolean,
        default: true,
    },
});

const emit = defineEmits(['close']);
const close = () => {
    if (props.closeable) {
        emit('close');
    }
};

</script>

<template>
    <teleport to="body">
        <div class="modal fade" :id="name" tabindex="-1">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div v-if="$slots.modalTitle" class="modal-header">
                        <slot name="modalTitle"/>
                    </div>
                    <div v-else class="modal-header">
                        <h5 class="modal-title">Modal title</h5>
                        <button type="button" class="btn-close" @click="close"></button>
                    </div>
                    <div class="modal-body">
                        <slot/>
                    </div>
                    <div v-if="$slots.modalFooter">
                        <slot name="modalFooter"/>
                    </div>
                    <div v-else>
                        <div class="modal-footer">
                            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                            <button type="button" class="btn btn-primary">Save changes</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </teleport>
</template>
