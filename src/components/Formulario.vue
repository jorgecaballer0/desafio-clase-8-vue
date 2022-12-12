<template>
  <div>
    <h1 class="text-center font-semibold text-2xl underline my-2">
      FORMULARIO - desafío clase 8
    </h1>
    <form id="formulario" @submit.prevent="validarForm" @submit="cargarUsuario">
      <div class="mb-4">
        <label for="email" class="block mb-2 text-sm font-medium text-gray-900"
          >NOMBRE</label
        >
        <input
          type="text"
          pattern="[A-z]{1,18}"
          id="nombre"
          aria-describedby="helper-text-explanation"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
          placeholder="Ingresá tu nombre (1-18 caracteres)"
          v-model.lazy.trim="nombre"
          required
        />
      </div>
      <div class="mb-4">
        <label for="email" class="block mb-2 text-sm font-medium text-gray-900"
          >EMAIL</label
        >
        <input
          type="email"
          pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,4}$"
          id="email"
          aria-describedby="helper-text-explanation"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
          placeholder="tucorreo@email.com"
          v-model.lazy.trim="email"
          required
        />
      </div>
      <div class="mb-4">
        <label for="email" class="block mb-2 text-sm font-medium text-gray-900"
          >TELÉFONO</label
        >
        <input
          type="tel"
          pattern="[0-9]{10}"
          id="telefono"
          aria-describedby="helper-text-explanation"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
          placeholder="Ingresá tu número de 10 dígitos"
          v-model.number.lazy="telefono"
          required
        />
      </div>
      <div class="mb-4">
        <label
          for="countries"
          class="block mb-2 text-sm font-medium text-gray-900"
          >GÉNERO</label
        >
        <select
          id="genero"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
          v-model="genero"
        >
          <option value="Seleccionar género" disabled>Seleccionar...</option>
          <option>Hombre</option>
          <option>Mujer</option>
          <option>Otro</option>
          <option>Prefiero no contestar</option>
        </select>
      </div>
      <div class="flex gap-4 justify-center">
        <button
          type="submit"
          class="bg-cyan-600 hover:bg-cyan-800 transition-colors rounded text-white p-2"
        >
          Enviar
        </button>
        <button
          @submit="limpiarForm"
          type="reset"
          class="bg-yellow-600 hover:bg-yellow-800 transition-colors rounded text-white p-2"
        >
          Reiniciar
        </button>
      </div>
    </form>
    <!-- TABLA -->
    <div>
      <div class="overflow-x-auto relative shadow-md sm:rounded-lg">
        <h1 class="text-center font-semibold text-2xl underline my-2">
          TABLA CON LOS DATOS
        </h1>
        <table class="w-full text-sm text-left text-gray-500">
          <thead class="text-xs text-gray-700 uppercase bg-gray-300">
            <tr>
              <th scope="col" class="py-3 px-6">NOMBRE</th>
              <th scope="col" class="py-3 px-6">EMAIL</th>
              <th scope="col" class="py-3 px-6">TELEFONO</th>
              <th scope="col" class="py-3 px-6">GÉNERO</th>
            </tr>
          </thead>
          <tbody>
            <tabla
              v-for="(usuario, i) of usuarios"
              :key="i"
              :usuarios="usuario"
            />
          </tbody>
        </table>
      </div>
      <div class="flex justify-center">
        <button
          class="bg-orange-600 hover:bg-orange-800 transition-colors rounded text-white p-2 my-3"
          v-on:click="limpiarTabla"
        >
          Limpiar último elemento
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import Tabla from "./Tabla.vue";

export default {
  components: { Tabla },
  name: "FormularioComponente",

  data() {
    return {
      nombre: "",
      email: "",
      telefono: "",
      genero: "",
      errores: [],
      usuarios: [],
    };
  },

  methods: {
    validarForm() {
      if (this.nombre && this.email && this.telefono && this.genero) {
        alert("Datos cargados correctamente");
        setTimeout(() => {
          document.getElementById("formulario").reset();
          (this.nombre = ""),
            (this.email = ""),
            (this.telefono = ""),
            (this.genero = "");
        }, 2000);
        return true;
      }
      if (!this.nombre) {
        this.errores.push("El nombre es obligatorio.");
      }
      if (!this.email) {
        this.errores.push("El email es obligatorio.");
      }
      if (!this.telefono) {
        this.errores.push("El telefono es obligatorio.");
      }
    },
    cargarUsuario() {
      let datos = {
        nombre: this.nombre,
        email: this.email,
        telefono: this.telefono,
        genero: this.genero,
      };
      this.usuarios.push(datos);
    },
    limpiarForm() {
      document.getElementById("formulario").reset();
      (this.nombre = ""),
        (this.email = ""),
        (this.telefono = ""),
        (this.genero = "");
    },
    limpiarTabla() {
      this.usuarios.pop();
      // Object.assign(this.$data, this.$options.data());
    },
  },
};
</script>
