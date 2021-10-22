<template>

  <section class="src-components-formulario jumbotron mt-1">
    <vue-form :state="formState" @submit.prevent="enviar()">

      <!-- Input de nombre -->
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

      <!-- Input de dni -->
      <validate tag="div">
        <label for="dni">Dni</label>
        <input type="number"
         id="dni" 
         name="dni" 
         class="form-control" 
         v-model="formData.dni"
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

      <!-- Input del monto -->
      <validate tag="div">
        <label for="monto">Monto</label>
        <input type="number"
         id="monto" 
         name="monto" 
         class="form-control"
         v-model.number="formData.monto" 
         autocomplete="off"
         readonly
         :style="{  }"
        >
      </validate>
      <br>

      <!-- Input de pago -->
      <validate tag="div">
        <label for="pago">Pago</label>
        <input type="number"
         id="pago" 
         name="pago" 
         class="form-control" 
         v-model.number="formData.pago"
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

    <div v-if="mostrar" class="table-responsive bg-dark">
      <h3 class="text-center">FACTURA {{pagos.length}}</h3>
      <table class="table">
        <tr>
          <th>Nombre</th>
          <th>Dni</th>
          <th>Monto a pagar</th>
          <th>Pago realizado</th>
          <th>Fecha</th>
          <th>Deuda</th>
        </tr>
        <tr>
          <th>{{ formData.nombre }}</th>
          <th>{{ formData.dni }}</th>
          <th>${{ formData.monto }}</th>
          <th>${{ formData.pago }}</th>
          <th>{{ formData.fecha }}</th>
          <th :style="{'background-color':calcularDeuda()==0 ? 'green':'red'}">${{ calcularDeuda() }}</th>
        </tr>
      </table>
    </div>
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
        mostrar: false,
        pagos: []
      }
    },
    methods: {
      getInitialData(){
        return {
          nombre: '',
          dni: null,
          monto: 10000,
          pago: 0,
          fecha: null
        }
      },
      calcularDeuda(){
        return this.formData.monto - this.formData.pago
      },
      enviar(){
        this.mostrar = true
        let hoy = new Date
        this.formData.fecha = hoy.toLocaleDateString()
        
        this.pagos.push(this.formData)
        console.log(this.pagos)
      },
    },
    computed: {

    }
}


</script>

<style lang="css">
  .src-components-formulario {

  }
  input{
    border: #000 !important;
  }
</style>
