<script>
import axios from "axios";

export default {
  name: "UserCreateView",
  data() {
    return {
      model: {
        usuario: {
          email: '',
          username: '',
          password: '',
          usuarioDetailDTO: {
            firstName: '',
            lastName: '',
            age: '',
            birthdate: ''
          }
        }
      }
    }
  },
  methods: {
    saveUser(e) {
      e.preventDefault();
      axios.post('http://localhost:8081/v1/usuarios?detailed=true', this.model.usuario)
          .then(res => {
            alert('User was saved successful');
            this.model.usuario = {
                email: '',
                username: '',
                password: '',
                usuarioDetailDTO: {
                  firstName: '',
                  lastName: '',
                  age: '',
                  birthdate: ''
                }
            }
          }).catch(function (error) {
            // hangle error on UI site
      })
    }
  }
}
</script>

<template>
  <div class="container mt-5">
    <form class="card">
      <div class="card-header">
        <h4>Add new user</h4>
      </div>
      <div class="card-body">
        <div class="mb-3">
          <label for="">First Name</label>
          <input min="2" max="10" type="text" v-model="model.usuario.usuarioDetailDTO.firstName" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Last Name</label>
          <input type="text" v-model="model.usuario.usuarioDetailDTO.lastName" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Email</label>
          <input type="email" v-model="model.usuario.email" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Age</label>
          <input type="text" v-model="model.usuario.usuarioDetailDTO.age" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Birthday</label>
          <input type="date" v-model="model.usuario.usuarioDetailDTO.birthdate" class="form-control">
        </div>

        <div class="mb-3">
          <label for="">Username</label>
          <input type="text" v-model="model.usuario.username" class="form-control">
        </div>

        <div class="mb-3">
          <label for="">Password</label>
          <input type="password" v-model="model.usuario.password" class="form-control">
        </div>

        <div class="mb-3">
          <button type="submit" @click="saveUser" class="btn btn-primary">
            Save
          </button>&nbsp;
          <RouterLink to="/usuarios" class="btn btn-dark">
            Back
          </RouterLink>
        </div>
      </div>
    </form>
  </div>
</template>

<style scoped>

</style>