<template>
  <h1 class="text-3xl font-bold underline text-center">
    Hello world!
  </h1>
  <Form/>
  <Modal/>
</template>

<script>
import Modal from './components/Modal.vue'
import Form from './components/Form.vue'
export default {

  name: 'App',
  components: {
    Modal,Form
  }
}
</script>

<style>
</style>
