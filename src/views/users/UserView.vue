<script>
import axios from "axios";

export default {
  name: "UserView",
  data() {
    return {
      users: []
    }
  },
  methods: {
    getUsers() {
      axios.get('http://localhost:8081/v1/usuarios?detailed=true').then(res => {
        this.users = res.data;
      }).catch(function (error) {
        // handle error on UI site
      })
    },

    deleteStudentById(studentId) {
      if (confirm('Are you sure, you want to delete this data?')) {
        axios.delete(`http://localhost:8081/v1/usuarios/${studentId}`).then(res => {
          this.getUsers();
        }).catch(function (error) {
          // handle error on UI site
        })
      }
    }
  },
  mounted() {
    this.getUsers();
  }


}
</script>

<template>
  <div class="course">
    <div class="card mt-5">
      <div class="card-header">
        <h4>
          Usuarios
          <RouterLink to="/usuarios/create" class="btn btn-primary float-end">
            Add New User
          </RouterLink>
        </h4>
      </div>
      <div class="card-body">
        <table class="table table-bordered">
          <thead>
            <tr>
              <th>Nro.</th>
              <th>Username</th>
              <th>Email</th>
              <th>First Name</th>
              <th>Last Name</th>
              <th>Age</th>
              <th>Birthday</th>
              <th>Actions</th>
            </tr>
          </thead>
          <tbody v-if="users.length > 0">
            <tr v-for="(student, index) in this.users" :key="index">
              <td>{{ index + 1 }}</td>
              <td>{{ student.username }}</td>
              <td>{{ student.email }}</td>
              <td>{{ student.usuarioDetailDTO.firstName }}</td>
              <td>{{ student.usuarioDetailDTO.lastName }}</td>
              <td>{{ student.usuarioDetailDTO.age }}</td>
              <td>{{ student.usuarioDetailDTO.birthdate }}</td>
              <td>
                <RouterLink :to="{ path: '/usuarios/' + student.id + '/edit' }" class="btn btn-success">
                  Edit
                </RouterLink>
                <button type="button" @click="deleteStudentById(student.id)" class="btn btn-danger">
                  Delete
                </button>
              </td>
            </tr>
          </tbody>
          <tbody v-else>
            <tr>
              <td colspan="7">There are no users</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>