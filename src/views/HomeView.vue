<template>
  <div class="home">
    <h1>Reactive vs Ref</h1>
    <h3>{{ iroman }}</h3>
    <h3>{{ hulk }}</h3>
    <button @click="changeIronman">Cambiar IronMan</button>
    <button @click="changeHulk">Cambiar Hulk</button>
    <h3>IronMan: {{ ironmanIsAlive }}</h3>
    <h3>Hulk: {{ hulkIsAlive }}</h3>
    <button @click="changeStatus">Cambiar Estado</button>
  </div>
</template>

<script>
import { ref, reactive } from 'vue'

export default {
  name: 'HomeView',
  setup(){
    const iroman = ref({name:'Tony', age:50})
    const hulk = reactive({name:'Bruce', age:50})
    const ironmanIsAlive = reactive(false)
    const hulkIsAlive = ref(true)
    const changeStatus = () => {
      hulkIsAlive.value = !hulkIsAlive.value
      ironmanIsAlive = !ironmanIsAlive // esto es un error Reactive funciona con objetos nada mas
    }
    return {
      iroman,
      hulk,
      ironmanIsAlive,
      hulkIsAlive,
      changeStatus,
      changeIronman: () => {
        iroman.value.name = 'Tony Stark'
        iroman.value.age = 55
      },
      changeHulk: () => {
        hulk.name = 'Bruce Banner'
        hulk.age = 45
      }
    }
  }
}
</script>
