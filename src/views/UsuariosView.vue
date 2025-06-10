<template>
  <div class="container py-4">
    <h2 class="mb-4">Usuarios desde MockAPI</h2>

    <table class="table table-dark table-bordered" v-if="usuarios.length">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Email</th>
          <th>Teléfono</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="usuario in usuarios" :key="usuario.id">
          <td>{{ usuario.nombre }}</td>
          <td>{{ usuario.email }}</td>
          <td>{{ usuario.telefono }}</td>
        </tr>
      </tbody>
    </table>

    <div v-else class="text-center mt-4">
      <p>Cargando usuarios...</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'UsuariosView',
  data() {
    return {
      usuarios: []
    }
  },
  mounted() {
    axios.get('https://68479ac1ec44b9f3493d83ca.mockapi.io/tp3-usuarios')
      .then(res => {
        this.usuarios = res.data
      })
      .catch(err => {
        console.error('Error al obtener usuarios:', err)
      })
  }
}
</script>
