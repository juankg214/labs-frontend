<template>
  <div class="col-12 col-sm-10 col-md-8 offset-sm-1 offset-md-2">
    <div class="mt-5">
        <div class="card shadow p-3 mb-5 bg-white rounded">
  <div class="card-body">
     <h2 class="col-12 text-center text-primary mt-3 mb-5">Roles del usuario</h2>
      <ul class="list-group " id="example-1">
          <!-- Por cada valor en roles, renderize una li con el texto que corresponde al nombre del rol -->
        <li class="list-group-item" v-for="rol in roles" :key="rol.id">{{ rol.roleName }}</li>
      </ul>
  </div>
</div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "showRole",
  data() {
    return {
      password: "",
      role: "",
      roles: []
    };
  },
  beforeCreate() {
    let associatePath = "/user/roles/"; //Path para acceder
    axios
      .get(this.$store.state.backURL + associatePath, { //Get al Back
        params: {
          access_token: localStorage.getItem("token") //Se pasa el token como parametro
        }
      })
      .then(response => {
        if (response.status !== 200) {
          alert("Error en la petición. Intente nuevamente");
        } else { // Si se realizo correctamente
          this.roles = response.data; // Se asigna la respuesta a la variable roles.
        }
      })
      .catch(response => {
        alert("No es posible conectar con el backend en este momento");
      });
  }
};
</script>

<style scoped>
    li{
        font-size: 20px;
    }
</style>
