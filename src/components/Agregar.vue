<template>
    <div>
        Hola
      <button @click="openModal">Agregar Película</button>
      <modal-component ref="modal"></modal-component>
    </div>
  </template>
  
  <script>
  import ModalComponent from './Modal.vue';
  
  export default {
    components: {
      ModalComponent,
    },
    methods: {
      openModal() {
        this.$refs.modal.openModal();
      }
    }
  };
  </script>
  