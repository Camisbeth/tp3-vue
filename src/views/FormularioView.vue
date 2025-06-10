<template>
  <div class="container py-4">
    <h2 class="mb-4">Formulario</h2>

    <form @submit.prevent="guardar" novalidate>
      <div class="form-group mb-3">
        <label>Nombre</label>
        <input
          type="text"
          class="form-control"
          v-model="nombre"
          @input="validarNombre"
        />
        <small v-if="errores.nombre" class="text-danger">{{ errores.nombre }}</small>
      </div>

      <div class="form-group mb-3">
        <label>Edad</label>
        <input
          type="number"
          class="form-control"
          v-model.number="edad"
          @input="validarEdad"
        />
        <small v-if="errores.edad" class="text-danger">{{ errores.edad }}</small>
      </div>

      <div class="form-group mb-3">
        <label>Email</label>
        <input
          type="email"
          class="form-control"
          v-model="email"
          @input="validarEmail"
        />
        <small v-if="errores.email" class="text-danger">{{ errores.email }}</small>
      </div>

      <button type="submit" class="btn btn-primary" :disabled="!formularioValido">Guardar</button>
    </form>

    <!-- Tabla de resultados -->
    <div v-if="usuarios.length" class="mt-5">
      <h4>Usuarios guardados</h4>
      <table class="table table-striped mt-3">
        <thead>
          <tr>
            <th>Nombre</th>
            <th>Edad</th>
            <th>Email</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(u, i) in usuarios" :key="i">
            <td>{{ u.nombre }}</td>
            <td>{{ u.edad }}</td>
            <td>{{ u.email }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nombre: '',
      edad: null,
      email: '',
      errores: {
        nombre: '',
        edad: '',
        email: ''
      },
      usuarios: []
    }
  },
  computed: {
    formularioValido() {
      return (
        !this.errores.nombre &&
        !this.errores.edad &&
        !this.errores.email &&
        this.nombre &&
        this.edad &&
        this.email
      )
    }
  },
  methods: {
    validarNombre() {
      if (!this.nombre) {
        this.errores.nombre = 'El nombre es obligatorio'
      } else if (this.nombre.length < 5 || this.nombre.length > 15) {
        this.errores.nombre = 'Debe tener entre 5 y 15 caracteres'
      } else {
        this.errores.nombre = ''
      }
    },
    validarEdad() {
      if (!this.edad) {
        this.errores.edad = 'La edad es obligatoria'
      } else if (this.edad < 18 || this.edad > 120) {
        this.errores.edad = 'Debe estar entre 18 y 120'
      } else {
        this.errores.edad = ''
      }
    },
    validarEmail() {
      const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
      if (!this.email) {
        this.errores.email = 'El email es obligatorio'
      } else if (!regex.test(this.email)) {
        this.errores.email = 'Debe ser un email válido'
      } else {
        this.errores.email = ''
      }
    },
    guardar() {
      if (this.formularioValido) {
        this.usuarios.push({
          nombre: this.nombre,
          edad: this.edad,
          email: this.email
        })
        // Limpiar
        this.nombre = ''
        this.edad = null
        this.email = ''
        this.errores = { nombre: '', edad: '', email: '' }
      }
    }
  }
}
</script>
