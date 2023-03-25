<template>
  <h1 id="#app">Holamundo</h1>
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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
