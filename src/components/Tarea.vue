<script setup>
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
            <button @click="cambiarEstado(tarea.id, 0)" :disabled="(tarea.estado == 0)" class="pendiente cambiarEstado"
                title="Pendiente">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    stroke="currentColor" class="size-6">
                    <path stroke-linecap="round" stroke-linejoin="round"
                        d="M9 15 3 9m0 0 6-6M3 9h12a6 6 0 0 1 0 12h-3" />
                </svg>
            </button>
            <button @click="cambiarEstado(tarea.id, 1)" :disabled="(tarea.estado == 1)" class="enProceso cambiarEstado"
                title="En proceso">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    stroke="currentColor" class="size-6">
                    <path stroke-linecap="round" stroke-linejoin="round"
                        d="M12 6v6h4.5m4.5 0a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
                </svg>
            </button>
            <button @click="cambiarEstado(tarea.id, 2)" :disabled="(tarea.estado == 2)" class="terminado cambiarEstado"
                title="Terminado">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    stroke="currentColor" class="size-6">
                    <path stroke-linecap="round" stroke-linejoin="round" d="m4.5 12.75 6 6 9-13.5" />
                </svg>
            </button>
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
    background-color: rgba(0, 17, 255, 0.707);
}

.enProceso {
    background-color: rgb(255, 255, 109);
}

.terminado {
    background-color: rgb(111, 255, 111);
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