<script>
import axios from "axios";

export default {
  name: "UserEditView",
  data() {
    return {
      usuarioId: '',
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
    getUserById(usuarioId) {
      axios.get(`http://localhost:8081/v1/usuarios/${usuarioId}`).then(res => {
        this.model.usuario = res.data;
      }).catch(function (error) {
        // handle error on UI site
      })
    },
    editUser() {
      axios.put(`http://localhost:8081/v1/usuarios/${this.usuarioId}`, this.model.usuario)
          .then(res => {
            alert('Usuario was Edited successful');
          }).catch(function (error) {
            // handle error on UI site
      })
    }
  },
  mounted() {
    this.usuarioId = this.$route.params.id;
    this.getUserById(this.usuarioId);
  }
}
</script>

<template>
  <div class="container mt-5">
    <div class="card">
      <div class="card-header">
        <h4>Edit User</h4>
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
          <button type="submit" @click="editUser" class="btn btn-primary">
            Save
          </button>&nbsp;
          <RouterLink to="/usuarios" class="btn btn-dark">
            Back
          </RouterLink>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>