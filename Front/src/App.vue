<script setup>
import { ref, onMounted } from 'vue'

// Variable reactiva para guardar la respuesta
const mensaje = ref('Cargando...')

// Función para obtener los datos del servidor Express
const obtenerMensaje = async () => {
  try {
    const respuesta = await fetch('http://localhost:3000/api/hola')
    const datos = await respuesta.json()
    mensaje.value = datos.mensaje
  } catch (error) {
    console.error('Error al conectar con el backend:', error)
    mensaje.value = 'Error al conectar con Express'
  }
}

// Ejecutar la petición cuando el componente se monta
onMounted(() => {
  obtenerMensaje()
})
</script>

<template>
  <main style="font-family: sans-serif; text-align: center; margin-top: 50px;">
    <h1>Conexión Vue + Express</h1>
    <p style="font-size: 1.5rem; color: #42b883;">
      {{ mensaje }}
    </p>
  </main>
</template>