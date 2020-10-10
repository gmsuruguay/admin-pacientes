<template>
  <div>
    <div class="container">
      <div class="row justify-content-md-center">
        <div class="col-md-5">
          <b-form @submit.prevent="login">
                <b-form-group
                  id="input-group-1"
                  label="Usuario"
                  label-for="input-1"        
                >
                  <b-form-input
                    id="input-1"         
                    type="text"
                    required     
                    v-model="usuario"     
                  ></b-form-input>
                </b-form-group>

                <b-form-group
                  id="input-group-2"
                  label="Password"
                  label-for="input-2"       
                >
                  <b-form-input
                    id="input-2"         
                    type="password"
                    required
                    v-model="password"
                  ></b-form-input>
              </b-form-group>       

            <b-button type="submit" variant="primary">Submit</b-button>      
          </b-form>
          <div class="alert alert-danger" role="alert" v-if="error">
            {{error_msg}}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    
  },
  data(){
    return{
      usuario :'',
      password :'',
      error: false,
      error_msg :''
    }
  },
  methods:{
    login(){
      let data = {
        usuario : this.usuario,
        password : this.password
      }
      let endpoint = "http://solodata.es/"
      axios.post(endpoint + "auth",data) 
      .then(response => {
        if (response.data.status == "ok") {
          localStorage.token = response.data.result.token
          this.$router.push('dashboard')
          this.error = false
        } else {
          this.error = true
          this.error_msg = response.data.result.error_msg
        }
      })
    }
  }
}
</script>
