<template>

  <section class="src-components-formulario jumbotron mt-1">
    <vue-form :state="formState" @submit.prevent="enviar()">

      <validate tag="div">
        <label for="nombre">Nombre</label>
        <input type="text"
         id="nombre" 
         name="nombre" 
         class="form-control"
         v-model.trim="formData.nombre"
         autocomplete="off"
         required
         :minlength="nombreMinLength"
         :maxlength="nombreMaxLength"
         no-espacios
        >

        <field-messages name="nombre" show="$dirty">

          <div slot="required" class="alert alert-danger mt-1">
            Campo requerido.
          </div>

          <div slot="no-espacios" class="alert alert-danger mt-1">
            El campo no puede contener espacios.
          </div>

          <div slot="minlength" class="alert alert-danger mt-1">
            Este campo requiere como mínimo {{ nombreMinLength }} caracteres.
          </div>

          <div v-if="formData.nombre.length == nombreMaxLength" class="alert alert-danger mt-1">
            Este campo acepta como máximo {{ nombreMaxLength }} caracteres.
          </div>

        </field-messages>
      </validate>
      <br>
      <validate tag="div">
        <label for="dni">Dni</label>
        <input type="number"
         id="dni" 
         name="dni" 
         class="form-control" 
         v-model.trim="formData.dni"
         autocomplete="off"
         required
         :minlength= "minDni"
         :maxlength= "maxDni"
        >

        <field-messages name="dni" show="$dirty">

          <div slot="required" class="alert alert-danger mt-1">
            Campo requerido
          </div>

          <div slot="minlength" class="alert alert-danger mt-1">
            Por favor, ingrese un DNI válido.
          </div>

          <div slot="maxlength" class="alert alert-danger mt-1">
            Por favor, ingrese un DNI válido.
          </div>

          <div v-if="formData.dni < 1000000" class="alert alert-danger mt-1">
            Por favor, ingrese un DNI válido.
          </div>

        </field-messages>
      </validate>
      <br>
      <validate tag="div">
        <label for="monto">Monto</label>
        <input type="number"
         id="monto" 
         name="monto" 
         class="form-control"
         v-model.trim="formData.monto" 
         autocomplete="off"
         readonly
        >
      </validate>
      <br>
      <validate tag="div">
        <label for="pago">Pago</label>
        <input type="number"
         id="pago" 
         name="pago" 
         class="form-control" 
         v-model.trim="formData.pago"
         autocomplete="off"
         required
         :min="minPago"
         :max="formData.monto"
        >

        <field-messages name="dni" show="$dirty">

          <div slot="required" class="alert alert-danger mt-1">
            Campo requerido
          </div>

          <div slot="min" class="alert alert-danger mt-1">
            El monto del pago debe ser positivo.
          </div>

          <div v-if="formData.pago > formData.monto" class="alert alert-danger mt-1">
            El pago no puede ser mayor al monto a abonar.
          </div>

        </field-messages>
      </validate>
      <br>

      <button class="btn btn-success my-3" :disabled="formState.$invalid">Enviar</button>

    </vue-form>

    <table v-if="mostrar" class="table">
      <tr>
        <th>Nombre</th>
        <th>Dni</th>
        <th>Monto a pagar</th>
        <th>Pago realizado</th>
        <th>Deuda</th>
      </tr>
      <tr>
        <th>{{formData.nombre}}</th>
        <th>{{formData.dni}}</th>
        <th>${{formData.monto}}</th>
        <th>${{formData.pago}}</th>
        <th :style="{'background-color':calcularDeuda()==0 ? 'green':'red'}">${{calcularDeuda()}}</th>
      </tr>
    </table>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-components-formulario',
    props: [],
    mounted () {

    },
    data () {
      return {
        formData: this.getInitialData(),
        formState: {},
        nombreMinLength: 3,
        nombreMaxLength: 15,
        minDni: 7,
        maxDni: 8,
        minPago: 1,
        mostrar: false
      }
    },
    methods: {
      getInitialData(){
        return {
          nombre: '',
          dni: null,
          monto: 10000,
          pago: 0,
        }
      },
      calcularDeuda(){
        return this.formData.monto - this.formData.pago
      },
      enviar(){
        this.mostrar = true;
        console.log(this.deuda)
      },
    },
    computed: {

    }
}


</script>

<style lang="css">
  .src-components-formulario {

  }
</style>
