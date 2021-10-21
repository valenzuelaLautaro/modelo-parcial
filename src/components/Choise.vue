<template>

  <section class="src-components-choise">
    <table class="table">
      <tr>
        <th>Numero de pregunta</th>
        <th>Respuesta</th>
      </tr>
      <tr v-for="(preg, index) in respuestas" :key="index">
        <td>{{ index+1 }}</td>
        <td>{{ preg }}</td>
      </tr>
    </table>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-components-choise',
    props: [],
    mounted () {

    },
    data () {
      return {
        respuestas: [ 'a' , 'a', 'b' ],
      }
    },
    methods: {  

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-choise {

  }
</style>
