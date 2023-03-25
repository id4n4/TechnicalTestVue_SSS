<template>
  <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
    <div class="mb-4">
      <label class="block text-sky-700 text-sm font-bold mb-2" for="email">
        Email
      </label>
      <input
        v-model="email"
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
        id="email"
        type="email"
        placeholder="Email"
      />
    </div>
    
    <div class="flex items-center justify-between">
      <button
        @click.prevent="enviarFormulario"
        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
        type="button"
      >
        Enviar
      </button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      nombre: '',
      email: '',
      mensaje: ''
    }
  },
  methods: {
    enviarFormulario() {
      // Aquí puedes guardar los datos del formulario en una base de datos o en un servidor
      // Luego, puedes mostrar los datos en un modal
      this.$emit('enviado', {
        nombre: this.nombre,
        email: this.email,
        mensaje: this.mensaje
      })
    }
  }
}
</script>


<style>

</style>