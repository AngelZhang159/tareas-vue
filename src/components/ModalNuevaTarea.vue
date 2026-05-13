<script setup>
import { ref } from 'vue';
import estadosTarea from "../data/tareas";

const emit = defineEmits(['close'])

const nombreTarea = ref("")
const descripcionTarea = ref("")
const estadoTareaSeleccion = ref(0)


function guardarTarea() {
    console.log(nombreTarea.value);
    console.log(descripcionTarea.value);
    console.log(estadoTareaSeleccion.value);
    let tareas = localStorage.getItem("tareas")
    let id = parseInt(localStorage.getItem("id"));
    if (!id) id = 0
    const tarea = {
        id: id,
        nombre: nombreTarea.value,
        descripcion: descripcionTarea.value,
        estado: estadoTareaSeleccion.value
    }
    localStorage.setItem("id", ++id)
    if (tareas == null) {
        localStorage.setItem("tareas", JSON.stringify([tarea]))
    } else {
        tareas = JSON.parse(tareas)
        tareas.push(tarea)
        localStorage.setItem("tareas", JSON.stringify(tareas))
    }
    emit('close')
}
</script>
<template>
    <div class="bg">
        <div class="modal">
            <header>
                <span class="titulo">
                    Crear nueva tarea
                </span>
                <button @click="$emit('close')" class="cerrar">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                        stroke="currentColor" class="size-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
                    </svg>
                </button>
            </header>
            <main>
                <div>
                    <label for="nombreTarea">Nombre de la tarea</label>
                    <input type="text" name="nombreTarea" v-model="nombreTarea">
                </div>
                <div>
                    <label for="descripcionTarea">Descripción</label>
                    <textarea name="descripcionTarea" v-model="descripcionTarea" rows="6"></textarea>
                </div>
                <div>
                    <label for="estadoTarea">Estado</label>
                    <div class="estadoTarea">
                        <button v-for="estado in estadosTarea" @click="estadoTareaSeleccion = estado.id"
                            :class="{ btnActivo: (estadoTareaSeleccion == estado.id) }">
                            {{ estado.nombre }}
                        </button>
                    </div>
                </div>
            </main>
            <footer>
                <button @click="guardarTarea()">Guardar</button>
            </footer>
        </div>
    </div>
</template>
<style scoped>
.btnActivo {
    background-color: rgb(40, 40, 40);
    color: white;
}

.estadoTarea {
    display: flex;
    flex-direction: row;
    justify-content: center;
    gap: 2rem;
}

button {
    font-size: 1.5rem;
    border-radius: .5rem;
    padding: .25rem .5rem;
}

footer {
    display: flex;
    flex-direction: row-reverse;
}

main,
div {
    display: flex;
    flex-direction: column;
    font-size: 1.5rem;
    gap: 1rem;
}

input,
textarea {
    font-size: 1.5rem;
    border-radius: .5rem;
    padding: .25rem .5rem;
}

textarea {
    resize: none;
}

header {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}

.titulo {
    font-weight: 900;
    font-size: 2rem;
}

.bg {
    z-index: 1;
    position: fixed;
    width: 100vw;
    height: 100vh;
    background-color: rgba(128, 128, 128, 0.518);
}

.cerrar {
    width: 3rem;
    height: 3rem;
    border-radius: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}

.modal {
    display: flex;
    flex-direction: column;
    border: 1px solid black;
    padding: 1rem;
    border-radius: 1rem;
    background-color: white;
    position: fixed;
    z-index: 999;
    top: 10%;
    left: 50%;
    width: 500px;
    margin-left: -250px;
    gap: 1rem;
    overflow-y: scroll;
}
</style>