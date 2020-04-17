<template>
  <div class="container">
    <div class="wrapper form-signin">
      <div class="col-sx-12 col-sm-12 col-md-12 col-lg-12">
        <div class="row">
          <div class="col-sx-12 col-sm-12 col-md-12 col-lg-12">
            <div class="col-sx-12 col-sm-12 col-md-12 col-lg-12 input-group mb-3">
              <div class="input-group-prepend">
                <h3>Formulario de registro</h3>
              </div>
            </div>
            <div class="col-sx-12 col-sm-12 col-md-12 col-lg-12 input-group mb-3">
              <div class="input-group-prepend">
                <h6>Todos los datos son obligatorios</h6>
              </div>
            </div>
            <div class="col-sx-12 col-sm-12 col-md-12 col-lg-12 input-group mb-3">
              <div class="input-group-prepend">
                <span class="input-group-text" id="basic-addon1">
                  <i class="fa fa-user-circle"></i>
                </span>
              </div>
              <input
                type="text"
                class="form-control"
                placeholder="Usuario"
                aria-label="Usuario"
                aria-describedby="basic-addon1"
                v-model="usuario"
              />
            </div>
            <div class="col-sx-12 col-sm-12 col-md-12 col-lg-12 input-group mb-3">
              <div class="input-group-prepend">
                <span class="input-group-text" id="basic-addon1">
                  <i class="fa fa-user"></i>
                </span>
              </div>
              <input
                type="text"
                class="form-control"
                placeholder="Nombre"
                aria-label="Nombre"
                aria-describedby="basic-addon1"
                v-model="nombre"
              />
            </div>
            <div class="col-sx-12 col-sm-12 col-md-12 col-lg-12 input-group mb-3">
              <div class="input-group-prepend">
                <span class="input-group-text" id="basic-addon1">
                  <i class="fa fa-at"></i>
                </span>
              </div>
              <input
                type="text"
                class="form-control"
                placeholder="Email"
                aria-label="Email"
                aria-describedby="basic-addon1"
                v-model="email"
              />
            </div>
            <div class="col-sx-12 col-sm-12 col-md-12 col-lg-12 input-group mb-3">
              <div class="input-group-prepend">
                <span class="input-group-text" id="basic-addon1">
                  <i class="fa fa-globe"></i>
                </span>
              </div>
              <input
                type="text"
                class="form-control"
                placeholder="Ciudad"
                aria-label="Ciudad"
                aria-describedby="basic-addon1"
                v-model="ciudad"
              />
            </div>
            <div class="col-sx-12 col-sm-12 col-md-12 col-lg-12 input-group mb-3">
              <div class="input-group-prepend">
                <span class="input-group-text" id="basic-addon1">
                  <i class="fa fa-whatsapp"></i>
                </span>
              </div>
              <input
                type="tel"
                class="form-control"
                pattern="[0-9]{3}-[0-9]{2}-[0-9]{3}"
                placeholder="Whatsapp"
                aria-label="Whatsapp"
                aria-describedby="basic-addon1"
                v-model="whatsapp"
                @keypress="validarNumeros($event)"
              />
            </div>
            <div class="col-sx-12 col-sm-12 col-md-12 col-lg-12 input-group mb-3">
              <div class="input-group-prepend">
                <span class="input-group-text" id="basic-addon1">
                  <i class="fa fa-lock"></i>
                </span>
              </div>
              <input
                type="password"
                class="form-control"
                placeholder="Contraseña"
                aria-label="Contraseña"
                aria-describedby="basic-addon1"
                v-model="contrasena"
              />
            </div>

            <div class="col-sx-12 col-sm-12 col-md-12 col-lg-12 input-group mb-3">
              <div class="input-group-prepend">
                <span class="input-group-text" id="basic-addon1">
                  <i class="fa fa-lock"></i>
                </span>
              </div>
              <input
                type="password"
                class="form-control"
                placeholder="Contraseña"
                aria-label="Contraseña"
                aria-describedby="basic-addon1"
                v-model="contrasena2"
              />
            </div>
            <div class="col-sx-12 col-sm-12 col-md-12 col-lg-12 input-group mb-3">
              <button
                type="submit"
                class="btn btn-primary col-sx-12 col-sm-12 col-md-12 col-lg-12 mb-3"
                @click="enviarDatos()"
              >Registrarme</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Swal from "sweetalert2";
import Axios from "axios";

export default {
  name: "HelloWorld",
  data() {
    return {
      usuario: "",
      nombre: "",
      email: "",
      ciudad: "",
      whatsapp: "",
      contrasena: "",
      contrasena2: "",
      params: {}
    };
  },
  methods: {
    validarNumeros: function(evt) {
      evt = evt ? evt : window.event;
      var charCode = evt.which ? evt.which : evt.keyCode;
      if (
        charCode > 31 &&
        (charCode < 48 || charCode > 57) &&
        charCode !== 46
      ) {
        evt.preventDefault();
      } else {
        return true;
      }
    },
    enviarDatos: function() {
      if (
        this.usuario.length === 0 ||
        this.nombre.length === 0 ||
        this.email.length === 0 ||
        this.ciudad.length === 0 ||
        this.whatsapp.length === 0 ||
        this.contrasena.length === 0 ||
        this.contrasena2.length === 0
      ) {
        Swal.fire("Revisión!", "Debe ingresar todos los datos obligatorios.");
        return;
      }
      var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      var emailValido = re.test(this.email);
      if (!emailValido && this.email.length > 0) {
        Swal.fire("Revisión!", "Debe ingresar un correo válido.");
        return;
      } else {
        this.params = {
          usuario: this.usuario,
          nombre: this.nombre,
          email: this.email,
          ciudad: this.ciudad,
          whatsapp: this.whatsapp,
          contrasena: this.contrasena
        };

        console.log(this.params);

        /*this.getJsonSave(this.params);*/

        Axios.post("", this.params)
          .then(response => {
            this.info = response.data.mensaje;

            Swal.fire("Registro exitoso!", "Bienvenido");

            /*limpiar formulario*/

            this.usuario = "";
            this.nombre = "";
            this.email = "";
            this.ciudad = "";
            this.whatsapp = "";
            this.contrasena = "";
            this.contrasena2 = "";
            this.info = null;
            this.loading = true;
            this.errored = false;
            this.params = {};
          })
          .catch(error => {
            console.log(error);
            this.errored = true;

            Swal.fire("Error al registrar", error);
          })
          .finally(() => (this.loading = false));
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
body {
  background: #eee !important;
  font-family: "Comic Sans MS", Arial, Times;
}

.wrapper {
  border-radius: 7%;
}

.form-signin {
  max-width: 380px;
  margin: 2% auto;
  text-align: center;
  padding: 2%;
  background-color: #fff;
  border: 1px solid rgba(0, 0, 0, 0.1);
}
</style>
