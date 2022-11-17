<template>

  <section class="src-components-usuarios">
   <div class="jumbotron">
    <h1>Muestra de usuarios</h1>
      <button class="btn btn-success my-3 mr-3" @click="getUsuariosFetch()">Fetch</button>
      <button class="btn btn-success my-3 mr-3" @click="getUsuariosAxios()">Axios</button>
      <button class="btn btn-warning my-3 mr-3" @click="borrar()">borrar</button>


      <!----------------------TABLA--------------------------------------------------------------->
      <div>
      <table class="table table-dark">
          <tr>
            <th>Nombre</th>
            <th>Email</th>
            <th>Edad</th>
          </tr>
          <tr v-for="usuario in usuarios" :key="usuario.email ">
            <td>{{usuario.nombre }}</td>
            <td>{{ usuario.email }}</td>
            <td>{{ usuario.edad }}</td>
          </tr>
        </table>
      </div>
   </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-components-usuarios',
    props: [],
    mounted () {
    
    },
    data () {
      return {
      ruta:"https://636d61cb91576e19e3273467.mockapi.io/Usuarios",
      usuarios:[]
      }
    },
    methods: {
      async getUsuariosAxios() {
        try {
          let post = await this.axios(this.ruta)
          this.usuarios = post.data
          if(this.usuarios.length == 0){
            alert("no hay usuarios disponibles")
          }
        }
        catch(error) { console.error(error) } 

      },
      borrar(){
        this.usuarios=[]
      },
      async getUsuariosFetch() {
        try {
          let response = await fetch(this.ruta)
          console.log(response)
          let respuesta = await response.json()
          this.usuarios = respuesta
          if(this.usuarios.length == 0){
            alert("no hay usuarios disponibles")
          }
        }
        catch(error) {
          console.error(error)
        }
      }

        },
    computed: {

    }
}


</script>

<style scoped lang="css">
.jumbotron{
  background-color: rgb(61, 62, 63);
  color: white;
}
.btn-success {
    color: #fff;
    background-color: #a9421d;
    border-color: #362923;
}

.btn-success:hover {
    color: #fff;
    background-color: #85513f;
    border-color: #362923;
}



</style>
