<template>
    <div>
        <Header/>        
        <div class="container">    
            <div :class="[status ? 'alert-success' : 'alert-danger', 'alert']" role="alert" v-if="status">
            {{mensaje}}
            </div>        
           <form>
                <div class="form-group">
                    <label for="inputDni">DNI</label>
                    <input type="text" class="form-control" id="exampleInputDni" v-model="paciente.dni">
                    
                </div>
                <div class="form-group">
                    <label for="inputNombre">Nombre</label>
                    <input type="text" class="form-control" id="inputNombre" v-model="paciente.nombre">
                </div>
                <div class="form-group">
                    <label for="inputTelefono">Teléfono</label>
                    <input type="text" class="form-control" id="inputTelefono" v-model="paciente.telefono">
                </div>
                
                <button type="button" class="btn btn-primary" @click="guardar()">Nuevo</button>
                
            </form>
        </div>

    </div>
</template>

<script>
import Header from '@/components/Header.vue'
import axios from 'axios'
    export default {
        name:'Nuevo',
        components:{
            Header
        },
        data(){
            return {
                status : false,
                mensaje : "", 
                paciente :{
                    "dni":"",
                    "nombre":"",
                    "telefono":"",
                    "token":"" 
                }
            }
        },
        methods:{
            guardar(){
                this.paciente.token = localStorage.getItem("token")
                axios.post("http://solodata.es/pacientes",this.paciente).then(result =>{
                   if(result.data.status == "ok"){
                       this.$router.push("/dashboard")
                   }else{
                       this.mensaje = "Error"
                   }
                })  
            }
        }
    }
</script>

<style lang="stylus" scoped>

</style>