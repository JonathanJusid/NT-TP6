<template>

  <section class="src-componentes-http">
    <div class="jumbotron">
      <h2>Usuarios</h2>
      <hr>
  <div v-if="cargoData">
      <div v-if="usuarios.length" class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Nombre</th>
            <th>Edad</th>
            <th>Email</th>
          </tr>
          <tr v-for="(usuario,index) in usuarios" :key="index">
            <td>{{usuario.nombre}}</td>
            <td>{{usuario.edad}}</td>
            <td>{{usuario.email}}</td>
          </tr>

        </table>
        <h4 class="alert alert-primary">Se encontraron {{usuarios.length}} usuarios</h4>
      </div>
      <h4 v-else class="alert alert-danger">No hay usuarios disponibles</h4>
    </div>
  </div> 
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-componentes-http',
    props: [],
    mounted () {
      this.getUsuariosAxios()
    },
    data () {
      return {
        url: 'https://60bf8fd397295a0017c43372.mockapi.io/usuarios', 
        usuarios : [],
        cargoData: false
      }
    },
    methods: {
      getUsuariosAxios() {
          this.axios(this.url)
          .then( respuesta => {
            this.usuarios = respuesta.data
            this.cargoData = true
          })
          .catch(error => console.error(error))
      }

    },
    computed: {
      getCols() {
        return Object.keys(this.usuarios[0])
      }
    }
}


</script>

<style scoped lang="css">
  .src-componentes-http {

  }

  .jumbotron {
    background: rgb(211,211,211); 
    color: white;
  }

  h2{
    color: black;
  }
     


  hr {
    background-color: #fff;
  }  
</style>