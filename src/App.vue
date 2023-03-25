<template>
  <h1 class="mb-4 text-4xl text-center font-extrabold leading-none tracking-tight text-gray-900 md:text-5xl lg:text-6xl dark:text-white">
    Prueba técnica desarrollador 
    <mark class="px-2 text-white bg-pink-600 rounded dark:bg-blue-500">Front-end</mark>
  </h1>
  <Form @submit="handleSubmit"/>
  <Modal @closeModal="closeModal" v-if="showModal"/>
</template>

<script>
import Modal from './components/Modal.vue'
import Form from './components/Form.vue'
export default {

  name: 'App',
  components: {
    Modal,Form
  },
  data() {
    return {
      formData: [],
      showModal: false
    }
  },
  methods: {
    handleSubmit(data) {
      this.formData = data
      for(let obj of data){
        console.log(obj.label + " => " + obj.input)
      }
      this.showModal = true;
    },
    closeModal(){
      this.showModal = false
    }
  }
}
</script>

<style>
</style>
