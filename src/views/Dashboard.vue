<template>
  <div>
   <Header/>
   <table class="table">
      <thead>
        <tr>          
          <th scope="col">Id</th>
          <th scope="col">DNI</th>
          <th scope="col">Nombre</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="paciente in listaPacientes" :key="paciente.PacienteId" @click="editar(paciente.PacienteId)">
          <th scope="row">{{paciente.PacienteId}}</th>
          <td>{{paciente.DNI}}</td>
          <td>{{paciente.Nombre}}</td>          
        </tr>       
      </tbody>
    </table>
  </div>
</template>

<script>  
 import Header from '@/components/Header.vue'
 import axios from 'axios'
  export default {
    name: "Dashboard",
    components:{
      Header
    },
    data() {
      return {        
        listaPacientes : null,
        nroPag : 1              
      }
    },
    mounted(){
      let nroPag = this.nroPag
      let endPoint = "http://solodata.es/pacientes?page="+nroPag
      axios.get(endPoint).then(result =>{
        console.log(result.data)
        this.listaPacientes = result.data
      })
    },
    methods: {
      editar(id) {
        console.log(id)
      },
    }
  }
</script>

<style scoped>

</style>