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
                
                <button type="button" class="btn btn-primary" @click="editar()">Editar</button>
                <button type="button" class="btn btn-info" @click="salir()">Salir</button>
            </form>
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
                status : false,
                mensaje : "",           
                paciente : {
                    "pacienteId":"",
                    "nombre" : "",
                    "dni" : "",                                    
                    "telefono" : "",
                    "token":""             
                    
                }
            }
        },
        mounted(){
            this.paciente.pacienteId = this.$route.params.id
            let endPoint = "http://solodata.es/pacientes?id="+this.paciente.pacienteId
            axios.get(endPoint).then(result =>{
                this.paciente.nombre = result.data[0].Nombre     
                this.paciente.dni = result.data[0].DNI     
                this.paciente.telefono = result.data[0].Telefono,
                this.paciente.token = localStorage.getItem("token")                         
            })
            //console.log(this.pacienteId)
        },
        methods:{
            editar(){
                axios.put("http://solodata.es/pacientes",this.paciente).then(result =>{
                   if(result.data.status == "ok"){
                       this.status=true
                       this.mensaje = "Updated success"
                   }else{
                       this.mensaje = "Error"
                   }                     
            })
            },
            salir(){
                this.$router.push("/dashboard")
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>