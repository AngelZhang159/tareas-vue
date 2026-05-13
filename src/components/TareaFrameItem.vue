<script setup>
import Tarea from './Tarea.vue';
import estadosTarea from "../data/tareas";


const tareas = JSON.parse(localStorage.getItem("tareas"))

const emit = defineEmits(['render'])

</script>
<template>
    <div v-for="tareasLista in estadosTarea" class="contenedorTarea">
        <h2 class="titulo">{{ tareasLista.nombre }}</h2>
        <div class="listaTareas">
            <template v-for="tarea in tareas">
                <Tarea v-if="tareasLista.id == tarea.estado" :tarea="tarea" @borrar="emit('render')"/>
            </template>
        </div>
    </div>
</template>
<style scoped>
.contenedorTarea {
    display: flex;
    flex-direction: column;
    align-items: center;
}
.titulo {
    border: 1px solid black;
    border-radius: 1rem;
    width: 15rem;
    height: 5rem;
    display: flex;
    justify-content: center;
    align-items: center;
}

.listaTareas {
    width: 25rem;
    display: flex;
    flex-direction: column;
    gap: 1rem;
}
</style>