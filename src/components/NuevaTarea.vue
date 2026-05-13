<script setup>
import { ref } from 'vue';
import ModalNuevaTarea from './ModalNuevaTarea.vue';

const mostrarModal = ref(false)

function cerrarModal() {
    mostrarModal.value = false
    emit('close')
}

const emit = defineEmits(['close'])
</script>
<template>
    <div>
        <button @click="mostrarModal = true">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                stroke="currentColor" class="size-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
            </svg>
            <span>Nueva tarea</span>
        </button>
    </div>
    <Teleport to="body">
        <ModalNuevaTarea v-if="mostrarModal" :mostrarModal="mostrarModal" @close="cerrarModal()" />
    </Teleport>
</template>
<style scoped>
svg {
    width: 3rem;
}

span {
    font-weight: 900;
    font-size: large;
    padding: .5rem 1rem;
}

button {
    padding: .5rem;
    border: 1px solid black;
    border-radius: 1rem;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: start;
}
</style>