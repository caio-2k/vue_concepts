<template>
  <h1>Lifecycle Hooks</h1>
</template>

<script>
import {onMounted} from 'vue'

// Hooks em composition API:
export default {
  
  //Função Hook
  setup () {
    onMounted(() => {
      console.log("Foi montado composition API")
    })
  }
  
}


// Hooks em options API:
// export default {
  //Iniciando métodos e lifecycle hooks

  //Hook mounted
//   mouted () {
//     console.log('Foi montado options API')
//   }

// }

</script>

<style>

</style>