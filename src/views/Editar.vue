<template>
    <div>
        <Header/>
        <div class="container">
            Editar
        </div>
    </div>
</template>

<script>
 import Header from '@/components/Header.vue'
 import axios from 'axios'

    export default {
        name:"Editar",
        components:{
            Header
        },
        data(){
            return{
                pacienteId: null,
                paciente : {
                    "nombre" : "",
                    "dni" : "",
                    "correo":"",
                    "codigoPostal" :"",
                    "genero" : "",
                    "telefono" : "",
                    "fechaNacimiento" : "",
                    "token" : "" , 
                    "pacienteId" : ""
                }
            }
        },
        mounted(){
            this.pacienteId = this.$route.params.id
            let endPoint = "http://solodata.es/pacientes?id="+this.pacienteId
            axios.get(endPoint).then(result =>{
                this.paciente.nombre = result.data[0].Nombre                
            })
            //console.log(this.pacienteId)
        }
    }
</script>

<style lang="scss" scoped>

</style>