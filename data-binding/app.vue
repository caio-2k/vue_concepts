<template>
  <div>
    <h1 :style="{ textDecoration: decoration }">Hello {{ name }}</h1>
    <!-- Qualquer propriedade do HTML pode ser uma prop que vá olhar dentro do meu model -->
     <!-- também posso escrever :style ao inves de v-bind:style -->
      <!-- Para vermos o two-way-data-binding funcionando, utilizaremos o input: -->
      <input type="text" v-model="name">
      <!-- Para isso utilizamos a diretiva v-model, que vincula o input com a prop que tá no 
      model, ou seja, quando o app iniciar, o vue vai olhar no data e vai pegar o que tá lá
      e o que tá sendo referenciado na diretiva e vice-versa -->
      <br>
      <a :href="link">Link para o curso!</a>
  </div>
</template>

<script>
export default {
  //Para termos um objeto que está interligado com a nossa view a gente
  //coloca no data, numa função que retorna um objeto.
  data: () => ({
    //Retorna um objeto que terá a propriedade name chamada Caio
    name: 'Caio',
    decoration: 'underline',
    link: 'https://treinamento.vuejsbrasil.org'
  })
};
</script>

<style>
</style>