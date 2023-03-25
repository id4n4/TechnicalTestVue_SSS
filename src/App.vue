<template>
  <h1 class="text-3xl font-bold underline text-center">
    Prueba técnica desarrollador front-end
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
