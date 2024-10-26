<template>
  <aside class="bg-base-200 w-72 min-h-screen">
    <h2 class="text-lg font-bold mx-4">Proyectos</h2>
    <p v-if="!proyectosStore.proyectos.length" class="text-sm text-gray-500 mx-4">No hay proyectos</p>

    <!-- Menu -->
    <ul class="menu">
      <li v-for="(proyecto, index) in proyectosStore.proyectos" :key="index">
        <a @click="selectProject(index)">{{ proyecto.nombre }}</a>
        <ul v-if="selectedProjectIndex === index" class="submenu">
          <li>Tareas completadas: {{ proyecto.tareas }}</li>
          <td>
            <progress :value="proyecto.progreso" class="progress progress-primary w-56" max="100"
              aria-label="Progreso del proyecto"></progress>
          </td>
          <li>
            Progreso: {{ proyecto.progreso.toFixed(0) }}% <!-- Mostrar porcentaje de progreso -->
          </li>
        </ul>
      </li>
    </ul>
  </aside>
</template>

<script lang="ts" setup>
import { useProyectosStore } from '../store/projects.store';
import { ref } from 'vue';

// Accediendo al store de proyectos
const proyectosStore = useProyectosStore();
const selectedProjectIndex = ref<number | null>(null);

// Función para seleccionar un proyecto
const selectProject = (index: number) => {
  // Alternar el submenú si el proyecto ya está seleccionado
  selectedProjectIndex.value = selectedProjectIndex.value === index ? null : index;
  console.log(`Seleccionaste el proyecto: ${proyectosStore.proyectos[index].nombre}`);
};
</script>

<style scoped>
.submenu {
  margin-left: 20px;
  /* Indentación del submenú */
  padding: 5px 0;
  /* Espaciado interno */
}
</style>
