<script setup>
import { ref } from 'vue';
import NuevaTarea from './components/NuevaTarea.vue';
import TareaFrameItem from './components/TareaFrameItem.vue';
import Titulo from './components/Titulo.vue';

const listaTarea = ref(null)
const tareasKey = ref(0);

function cerrar() {
  tareasKey.value += 1
}
</script>

<template>
  <header>
    <Titulo msg="App Tareas" />
    <NuevaTarea @close="cerrar()" />
  </header>

  <main>
    <TareaFrameItem :key="tareasKey" @render="cerrar()"/>
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-direction: row;
  width: 100vw;
  gap: 2rem;
  justify-content: space-evenly;
}
header {
  line-height: 1.5;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  padding-inline: 5rem;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

</style>
