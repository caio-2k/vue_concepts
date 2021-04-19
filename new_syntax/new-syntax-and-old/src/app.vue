<template>
  <div>
    <h1>Minha lista de tarefas</h1>
    <button @click="handleShowList()">Ver a Lista!</button>
    <br />

    <input 
    type="text" 
    v-focus 
    v-model="state.currentTask"
    @keyup.enter="addTask"
    >

    <ul v-if="state.showList">
      <li v-for="(task, index) in state.tasks"
       @dblclick="complete(task)"
       :class="{ 'line-through': task.isDone }"
       class="task-item"
       :key="`${task}-${index}`">
        {{ task.name }}
        <button @click="remove(task)">&times;</button>
      </li>
    </ul>
    <p v-else>Lista de tarefas está escondida, clique no botão!</p>
  </div>
</template>

<script>
import { reactive } from 'vue'

// Componente
const focus = {
  inserted: (el) => {
    el.focus();
  },
};

export default {
  directives: {
    focus,
  },
  setup () {
    //Criando objeto reativo, cria um var state e nela chama a func reactive
    //e dentro da função coloco o código do objeto que quero que se torne reativo
    const state = reactive({
    currentTask: '',
    showList: false,
    tasks: [{ name: "Fazer o curso", isDone: false }],
  })

  //Métodos:

  function handleShowList() {
      state.showList = !state.showList;
    }

    function complete(task) {
      state.tasks = state.tasks.map((t) => {
        if (t.name === task.name) {
          return { ...t, isDone: !t.isDone };
        }
        return { ...t };
      });
    }

    function remove(task) {
      state.tasks = state.tasks.filter((t) => t.name !== task.name);
      console.log("task", task);
    }

    function addTask(){
      state.tasks.push({
        name: state.currentTask,
        isDone: false,
      })
      state.currentTask = ''
    }

    return {
      state,
      //Retornando os métodos
      handleShowList,
      addTask,
      complete,
      remove,
    }
  }
}

</script>

<style scoped>
.line-through {
  text-decoration: line-through;
}
.task-item{
  cursor: pointer;
}
</style>