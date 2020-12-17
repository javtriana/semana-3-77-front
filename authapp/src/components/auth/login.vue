<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container">
        <a class="navbar-brand" href="#">Acceso Usuarios</a>
      </div>
    </nav>

    <div class="container">
      <div class="row">
        <div class="col-lg-6 offset-lg-3 col-sm-10 offset-sm-1">
          <form
            class="text-center border border-dark p-5 bg-light"
            style="margin-top: 70px; height: auto; padding-top: 40px !important"
            @submit.prevent="loginUser"
          >
            <h1 class="h3 mb-3 font-weight-normal" style="text-align: center">
              Inicio de sesión
            </h1>
            <input
              type="text"
              id="email"
              class="form-control mb-3"
              placeholder="Email"
              v-model="login.email"
            />
            <!-- Password -->
            <input
              type="password"
              id="password"
              class="form-control mb-5"
              placeholder="Contraseña"
              v-model="login.password"
            />
            <!-- inicio sesion button -->
            <center>
              <button
                class="btn btn-lg btn-primary btn-block w-100 my-7 bg-info border-light"
                type="submit"
              >
                Entrar
              </button>
            </center>
          </form>
        </div>
      </div>
    </div>


    <nav
      class="navbar fixed-bottom navbar-light bg-dark"
      style="padding-top: 20px"
    >
      <div class="container">
        <span class="navbar-text text-light">
          login area ©grupo77, aplicación de login de usuario, Frontend
        </span>
      </div>
    </nav>



  </div>
</template>
<script>
import swal from "sweetalert";
export default {
  data() {
    return {
      login: {
        email: "",
        password: "",
      },
    };
  },
  methods: {
    async loginUser() {
      try {
        let response = await this.$http.post("/api/auth/signin", this.login);
        console.log(response.data);
        let token = response.data.accessToken;
        localStorage.setItem("jwt", token);
        if (token) {
          swal("Exitoso", "login exitoso", "success");
          this.$router.push("/home");
        }
      } catch (err) {
        swal("Error", "datos incorrectos", "error");
        console.log(err.response);
      }
    },
  },
};
</script>