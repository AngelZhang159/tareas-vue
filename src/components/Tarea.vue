<script setup>
import tareas from '@/data/tareas'

defineProps({
    tarea: {
        type: Object,
        required: true
    }
})
const emit = defineEmits(['borrar'])

function borrarTarea(id) {
    if (confirm("¿Borrar tarea?")) {
        let tareas = JSON.parse(localStorage.getItem("tareas"))

        tareas = tareas.filter(e => e.id != id)
        localStorage.setItem("tareas", JSON.stringify(tareas))
        emit('borrar')
    }
}

function cambiarEstado(id, estadoNuevo) {
    let tareas = JSON.parse(localStorage.getItem("tareas"))
    tareas.forEach(e => {
        if (e.id == id) {
            e.estado = estadoNuevo
        }
    });
    localStorage.setItem("tareas", JSON.stringify(tareas))
    emit('borrar')
}
</script>
<template>
    <div class="bg" :name="tarea.id" draggable="true" id="tarea">
        <div>
            <span>
                {{ tarea.nombre }}
            </span>
            <p>
                {{ tarea.descripcion }}
            </p>
        </div>
        <div>
            <button class="eliminar" @click="borrarTarea(tarea.id)" title="Eliminar tarea">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    stroke="currentColor" class="size-1">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
                </svg>
            </button>
            <template v-for="tareaItem in tareas">
                <button @click="cambiarEstado(tarea.id, tareaItem.id)" :disabled="(tarea.estado == tareaItem.id)"
                    class="cambiarEstado" :style="{ backgroundColor: tareaItem.color }" :title="tareaItem.nombre">
                    <img :src="tareaItem.icono">
                </button>
            </template>
        </div>
    </div>
</template>
<style scoped>
.eliminar {
    background-color: red;
}

.eliminar:hover {
    background-color: rgb(150, 0, 0);
}

.eliminar:active {
    background-color: rgb(69, 0, 0);
}

.bg {
    background-color: rgb(186, 186, 186);
    border-radius: 1rem;
    padding: 1rem;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}

span {
    font-weight: 700;
    font-size: medium;
}

p {
    font-weight: 100;
    font-size: small;
}

.pendiente {
    background-color: #0011ffb4;
}

.enProceso {
    background-color: #ffff6d;
}

.terminado {
    background-color: #6fff6f;
}


button {
    border-radius: .5rem;
    width: 1.75rem;
    height: 1.75rem;
    display: flex;
    justify-content: center;
    align-items: center;
}

button svg {
    width: 1rem;
    height: 1rem;
    color: black;
}
</style>