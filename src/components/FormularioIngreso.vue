<template>

  <section class="src-components-formulario">
    <div class="jumbotron">
      <h2>Formulario</h2>
      <hr>
      <hr>
      <br>
    <vue-form :state="formState" @submit.prevent="enviar()">
        <!-- ----------------------------------- -->
        <!--            CAMPO NOMBRE             -->
        <!-- ----------------------------------- -->
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input 
            type="text" 
            id="nombre" 
            class="form-control" 
            autocomplete="off"
            v-model.trim="formData.nombre"
            name="nombre" 
            required
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"
          >
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="minlength" class="alert alert-danger mt-1">Este campo debe poseer al menos {{ nombreMinLength }} caracteres</div>
            <div slot="no-espacios" class="alert alert-danger mt-1">Este campo puede poseer hasta {{ nombreMaxLength }} caracteres</div>
          </field-messages>
        </validate>        

        <br>

        <!-- ----------------------------------- -->
        <!--            CAMPO EDAD               -->
        <!-- ----------------------------------- -->
        <validate tag="div">
          <label for="edad">Edad</label>
          <input 
            type="number" 
            id="edad" 
            class="form-control" 
            autocomplete="off"
            v-model.number="formData.edad"
            name="edad" 
            required
            :min="edadMinima"
            :max="edadMaxima"
          >
          <field-messages name="edad" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="min" class="alert alert-danger mt-1">La edad minima es de {{ edadMinima }}</div>
            <div slot="max" class="alert alert-danger mt-1">La edad maxima es de {{ edadMaxima }}</div>
          </field-messages>
        </validate>    

        <br>

        <!-- ----------------------------------- -->
        <!--            CAMPO EMAIL              -->
        <!-- ----------------------------------- -->
        <validate tag="div">
          <label for="email">Email</label>
          <input 
            type="email" 
            id="email" 
            class="form-control" 
            autocomplete="off"
            v-model.trim="formData.email"
            name="email" 
            required
          > 
          <field-messages name="email" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="email" class="alert alert-danger mt-1">Email no válido</div>
          </field-messages>
        </validate>    

        <br>

        <button class="btn btn-success my-3" :disabled="formState.$invalid">Enviar</button>
      </vue-form>

      <hr>

      <div class="media alert alert-info" v-for="(dato,index) in datos" v-bind:key="index">
          <div class="media-body">
              <br>
              <p>Nombre: {{ dato.nombre }}</p>
              <p>Edad: {{ dato.edad }}</p>
              <p>Email: {{ dato.email }}</p>
          </div>
      </div>
    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-components-http-client',
    props: [],
    mounted () {

    },
    data () {
      return {
        formData: this.getInitialData(),
        formState: {},
        nombreMinLength: 3,
        nombreMaxLength: 15,
        edadMinima: 18,
        edadMaxima: 120,
        datos: [],
        ruta:"https://636d61cb91576e19e3273467.mockapi.io/Usuarios"

      }
    },
    methods: {
      getInitialData() {
        return {
          nombre: null,
          edad: null,
          email: null
        }
      },
      enviar() {
      this.cargarDatos({ ...this.formData })
    

      this.formData = this.getInitialData();
      this.formState._reset();
    },
    async cargarDatos(usuario){
      try {
          await this.axios.post(this.ruta,usuario)
        }
        catch(error) { console.error(error) } 
        
    }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .jumbotron {
  background-color: rgb(61, 62, 63);
  color: white;
}

hr {
  background-color: #bbb;
}

.btn-success.disabled, .btn-success:disabled {
    color: #fff;
    background-color: #a9421d;
    border-color: #362923;
}
</style>