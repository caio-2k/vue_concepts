<template>
  <div>
    <h1>Minha lista de tarefas</h1>
    <button @click="() => (showList = !showList)">Ver a Lista!</button>
    <br>
    <!-- Criando diretiva propria -->
    <input type="text" v-focus>
    <ul v-if="showList">
      <!-- Com o v-if não irá aparecer a lista pois está como false -->
      <li v-for="(task, index) in tasks" :key="`${task}-${index}`">
        <!-- v-for é uma diretiva de iteração -->
        <!-- O valor não pode se repetir, como não tem index, fazemos assim -->
        {{ task.name }}
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
    el.focus()
  }
}

// Componente:
export default {
  // Registrando diretiva
  directives: {
    focus,
  },
  data: () => ({
    showList: false,
    tasks: [{ name: "Fazer o curso", isDone: false }],
  }),
};
</script>