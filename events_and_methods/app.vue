<template>
  <div>
    <h1>Minha lista de tarefas</h1>
    <!-- Vai disparar ao clicar -->
    <button @click="handleShowList()">Ver a Lista!</button>
    <br />
    <!-- Criando diretiva propria -->

    <input 
    type="text" 
    v-focus 
    v-model="currentTask"
    @keyup.enter="addTask"
    >

    <ul v-if="showList">
      <!-- Com o v-if não irá aparecer a lista pois está como false -->
      <!-- v-for é uma diretiva de iteração -->
      <li v-for="(task, index) in tasks"
       @dblclick="complete(task)"
       :class="{ 'line-through': task.isDone }"
       class="task-item"
       :key="`${task}-${index}`">
       <!-- O valor não pode se repetir, como não tem index, fazemos assim -->
        <!-- Registrando um evento de duplo clique -->
        <!-- v-bind para colocar a classe line-through quando a task for true -->
        {{ task.name }}
        <!-- método remove passando um param task que estou percorrendo no v-for -->
        <button @click="remove(task)">&times;</button>
        <!-- Ao rodar vai aparecer: "Fazer o curso" -->

      </li>
    </ul>
    <!-- Se eu quiser a condição oposta ao v-if anterior: -->
    <p v-else>Lista de tarefas está escondida, clique no botão!</p>
  </div>
</template>

<script>
// Criando diretiva propria
const focus = {
  // Quando a diretiva é inserida, recebo alguns params (el = element)
  inserted: (el) => {
    el.focus();
  },
};

// Componente:
export default {
  // Registrando diretivas
  directives: {
    focus,
  },

  data: () => ({
    currentTask: '',
    showList: false,
    tasks: [{ name: "Fazer o curso", isDone: false }],
  }),

  //Registrando métodos
  methods: {
    handleShowList() {
      // para acessarmos um método dentro de um método, precisamos de this
      this.showList = !this.showList;
    },
    complete(task) {
      // Agora vou chamar o map, não o filter, pois não vou remover nada da lista
      // (filtrar), vou ter a mesma list mas com o isDone falso ou true
      this.tasks = this.tasks.map((t) => {
        if (t.name === task.name) {
          return { ...t, isDone: !t.isDone };
        }
        return { ...t };
      });
    },
    remove(task) {
      // Criando um array novo para remover, filtra o array coloca todo mundo de volta
      // no array, menos o da comparação
      this.tasks = this.tasks.filter((t) => t.name !== task.name);
      console.log("task", task);
    },
    addTask(){
      //Tenho um array, colocar mais um item no array e depois zerar meu currentTask
      //par ao input ficar vazio
      this.tasks.push({
        name: this.currentTask,
        isDone: false,
      })
      this.currentTask = ''
    }
  },
};
</script>

<style scoped>
.line-through {
  text-decoration: line-through;
}
.task-item{
  cursor: pointer;
}
</style>