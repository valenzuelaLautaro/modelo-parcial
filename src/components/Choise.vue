<template>

  <section class="src-components-choise ">
    <div class="table-responsive jumbotron mt-1">
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
    </div>
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

<style lang="css">
  .src-components{

  }
  .jumbotron{
    background-color: blueviolet;
  }
  th{
    color: #fff;
  }
  td{
    color: #fff;
  }
</style>
