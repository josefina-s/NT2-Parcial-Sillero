<template>

  <section class="src-componentes-tabla">
    <div class="jumbotron">
      <h2>Respuestas</h2>
      
      <br/>
      <table class="table table-dark">
          <tr>
            <th>Numero de pregunta</th>
            <th>Respuesta</th>
          </tr>
          <tr v-for="(pregunta, index) in preguntas"
              :key="index">
            <td>{{ pregunta.numero }}</td>
            <td>{{ pregunta.respuestas }}</td>
          </tr>
          
        </table>
      <br>
    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-tabla',
    props: [],
    mounted () {

    },
    data () {
      return {
        preguntas : [
          {numero : 1, respuestas : ['b', 'd']},
          {numero : 2, respuestas : ['c']},
          {numero : 1, respuestas : ['b', 'e']},
        ]
      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .jumbotron {
  background-color: rgb(196, 196, 196);
}
</style>
