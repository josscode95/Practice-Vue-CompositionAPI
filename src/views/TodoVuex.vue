<template>
  <h1>Thanos Todo List</h1>
  <!-- <h4>Pendientes: {{ $store.state.todos.filter(t => !t.completed).length }}</h4> -->
  <h4>Pending: {{ pending.length }}</h4>
  <hr>
  <button 
    :class="{ 'active': currentTab === 'all' }"
    @click="currentTab = 'all'"
  >
    Todos
  </button>
  <button 
    :class="{ 'active': currentTab === 'pending' }"
    @click="currentTab = 'pending'"
  >
    Pendientes
  </button>
  <button 
    :class="{ 'active': currentTab === 'completed' }"
    @click="currentTab = 'completed'"
  >
    Completados
  </button>
  <div>
    <ul>
      <li 
        v-for="todo in getTodosByTab" :key="todo.id"
        :class="{ 'completed': todo.completed === true }"
        @dblclick="toggleTodo(todo.id)"
      >
        {{ todo.text }}
      </li>
    </ul>
  </div>
  <button @click="isOpen = true">Crear Todo</button>
  <modal 
    v-if="isOpen"
    @on:close="isOpen = false"
  >
    <template v-slot:header>
      <h1>Nueva Tarea</h1>
    </template>
    <template v-slot:body>
      <form>
        <input 
          type="text" 
          placeholder="Nueva tarea"
        >
      </form>
      <br>
      <br>
      <button type="submit">Crear</button>
    </template>
  </modal>
</template>

<script>
import useTodos from '@/composables(hooks)/useTodo'
import Modal from '@/components/Modal.vue'
import { ref } from '@vue/reactivity'
export default {
  components: { Modal },
  setup(){
    const { 
      currentTab, 
      getTodosByTab, 
      pending, 
      toggleTodo,
    } = useTodos()
    return {
      currentTab,
      getTodosByTab,
      pending,
      toggleTodo,

      isOpen: ref(false)
    }
  }
}

</script>

<style scoped>
  div{
    display: flex;
    justify-content: center;
    text-align: center;
  }
  ul{
    width: 300px;
    text-align: left;
  }
  li, button{
    cursor: pointer;
  }
  .active{
    background-color: #2c3e50;
    color: white;
  }
  .completed{
    text-decoration: line-through;
  }
</style>