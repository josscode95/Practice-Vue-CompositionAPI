<template>
  <h1>Aprendiendo Slots</h1>
  <button @click="openModal">Abrir modal</button>
  <!-- Un slot es como el Hight Order Component de React -->
  <modal
    title="Hola Mundo"
    v-if="isOpen"
    @on:close="closeModal"
  >
    <!-- <p>Lorem ipsum dolor sit amet consectetur adipisicing elit.</p>
    <button>Salir</button>
    <h2>Titulo del modal</h2> -->
    <template v-slot:body>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit.</p>
    </template>
    <template v-slot:footer>
      <button @click="closeModal">Salir</button>
    </template>
    <template v-slot:header>
      <h2>Titulo del modal</h2>
    </template>
    <template v-slot:exposed="{ newTitle }">
      <h3>{{ newTitle }}</h3>
    </template>
  </modal>
</template>

<script>
import Modal from '@/components/Modal.vue'
import { ref } from 'vue'

export default {
  components: { Modal },
  setup(){

    const isOpen = ref(false)

    return{
      isOpen,
      openModal: () => isOpen.value = true,
      closeModal: () => isOpen.value = false
    }

  }
}

</script>

<style>

</style>