<template >
  <div>
    <Navigator />
    <div class="LogReg">
      <div class="log-reg-cont">
        <div class="login">
          <div class="login-cont">
            <p class="titulo-lr">INICIAR SESIÓN</p> 
            <form @submit.prevent="login(emailL, password)">
              <div >
                <div class="input-lr-c">
                  <label for="">Email</label>
                  <input
                    v-model="emailL"
                    type="text"
                    name="email"
                    id="email"
                    class="input-txt-lr"
                  />
                </div>

                <div class="input-lr-c">
                  <label for="">Contraseña</label>
                  <input
                    v-model="password"
                    :type="type3"
                    name="contrasena"
                    id="contrasena"
                    class="input-txt-lr"
                  />
                    <p @click="type3 == 'password' ? type3 = 'text' : type3 = 'password'" class="pointer showpass">Mostrar contraseña</p>
                </div>
              </div>
              <input type="submit" value="INICIAR SESIÓN" class="btn-lr" />
              <div v-if="status2 != ''" class="status_messages">
                <div v-if="status2 == 'success'" class="msg msg_success">
                  <p>{{ message2 }}</p>
                </div>
                <div v-if="status2 == 'error'" class="msg msg_error">
                  <p>{{ message2 }}</p>
                </div>
              </div>
            </form>
          </div>
        </div>
        <div class="registro">
          <div class="registro-cont">
            <p class="titulo-lr">CREAR CUENTA</p>
            <p class="ryobe">Regístrate y obtén beneficios exclusivos.</p>

            <form
              @submit.prevent="
                submit(name, lastname, email, phone, pass, passc)
              "
            >
              <div class="m-btm">
                <div class="input-lr-c">
                  <label for="">Nombre(s)</label>
                  <input
                    type="text"
                    name="name"
                    id="name"
                    v-model="name"
                    class="input-txt-lr"
                  />
                </div>
                <div class="input-lr-c">
                  <label for="">Apellido(s)</label>
                  <input
                    type="text"
                    name="lastname"
                    id="lastname"
                    v-model="lastname"
                    class="input-txt-lr"
                  />
                </div>
                <div class="input-lr-c">
                  <label for="">Email</label>
                  <input
                    type="text"
                    name="email"
                    id="email"
                    v-model="email"
                    class="input-txt-lr"
                  />
                </div>
                <div class="input-lr-c">
                  <label for="">Telefono</label>
                  <input
                    type="text"
                    name="phone"
                    id="phone"
                    v-model="phone"
                    class="input-txt-lr"
                  />
                </div>
                <div class="input-lr-c">
                  <div class="contra-cont">
                    <label for="">Contraseña</label>
                    <input
                      :type="type1"
                      name="pass"
                      id="pass"
                      v-model="pass"
                      class="input-txt-lr"
                    />
                    <p @click="type1 == 'password' ? type1 = 'text' : type1 = 'password'" class="pointer showpass">Mostrar contraseña</p>
                    <label for="" v-if="pass.length > 0"
                      >Confirmar Contraseña</label
                    >
                    <input
                      :type="type2"
                      name="passc"
                      id="passc"
                      v-model="passc"
                      class="input-txt-lr"
                      v-if="pass.length > 0"
                    />
                    <p @click="type2 == 'password' ? type2 = 'text' : type2 = 'password'" v-if="pass.length > 0" class="pointer showpass">Mostrar contraseña</p>
                  </div>
                </div>
              </div>
              <div class="acepts-adv">
                <input type="checkbox" id="checkbox" v-model="terms" name="" />
                <label for="checkbox"
                  >He leído y estoy de acuerdo con los
                  <a href="">Terminos de Servicio</a> y
                  <a href="">Política de Privacidad</a>.</label
                >
              </div>
              <input type="submit" value="REGISTRAR" class="btn-lr" />
              <div v-if="status != ''" class="status_messages">
                <div v-if="status == 'success'" class="msg msg_success">
                  <p>{{ message }}</p>
                </div>
                <div v-if="status == 'error'" class="msg msg_error">
                  <p>{{ message }}</p>
                </div>
              </div>
            </form> 
          </div>
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>
<script>
import userService from '../services/user.service'
import Navigator from "../components/Navigator";
import Footer from "../components/Footer";
import { url, endpointCodes } from "../global/index";
import { mapActions } from "vuex";
export default {
  components: {
    Navigator,
    Footer,
  },
  data() {
    return {
      terms: false,
      status: "",
      message: "",
      status2: "",
      message2: "",
      name: "",
      lastname: "",
      role: "cliente",
      phone: "",
      email: "",
      pass: "",
      passc: "",
      emailL: "",
      password:'',
      type1: 'password',
      type2: 'password',
      type3: 'password',
    };
  },
      metaInfo(){
        return{
            title: 'Iniciar sesión',
            titleTemplate: "%s | Agriga de México",
            htmlAttrs: {
            lang: "es",
            },
            meta: [
            { charset: "utf-8" },
            {
                name: "description",
                content: "Regístrate o ingresa en Agriga de México y obtén beneficios exclusivos.",
            },
            { name: "viewport", content: "width=device-width, initial-scale=1" },
            ],            
        };
      },
  async created() {
    await this.obtenerCarritos();
  },
  computed:{
    carrito() {
      return this.$store.getters["carrito/getcar"];
    },
    update() {
      return this.$store.getters["carrito/getupd"];
    },
  },
  methods: {
    ...mapActions("usuarios", ["setAddedUsr"]), 
    ...mapActions("carrito", ["getCart"]),
    ...mapActions("carrito", ["getCartCopy"]),
    wait: function () {
      setTimeout(() => this.$router.go(), 200);
    },   
    async obtenerCarritos() {
      await this.getCart();
      await this.getCartCopy();
    }, 

      delStatus: function () {
      setTimeout(() => this.delMsgs()
      ,1500);
    },
    delMsgs: function(){
       this.status=""
       this.message=""
    },
    submit: async function (name, lastname, email, phone, password, passc) {
      this.status = "";
      this.message = "";
      
      if (this.terms === true) {
      if (password === passc) {
        let usuario = {
          name: name,
          lastname: lastname,
          role: 'cliente',
          email: email,
          phone: phone,
          password: password,
        };

        let result = await this.$store.dispatch("usuarios/addItemUsr2", {
          option: "user-register",
          item: usuario,
        });
        console.log(result)
        if (result.status == "error") {
          this.status = "error";
          this.message = result.message;
        } else {
          // success
          this.setAddedUsr(result.added);
          this.Add();
          this.status = "success";
          this.message = "Se ha registrado el usuario. Ahora inicia sesión.";
        }
      } else {
        this.status = "error";
        this.message = "Las contraseñas no coinciden.";
      }
      } else {
        this.status = "error";
        this.message = "Debes aceptar los Términos de Servicio y Política de Privacidad.";
      }
    },

    async login(email, password) {
      this.status = "";
      this.message = "";

      let result = await this.$store.dispatch("admin/login", {
        email,
        password,
      });

      if (result.status == "success") {
        let response = await this.$store.dispatch("admin/getData");

        if (response.status == "success") {
          if (
            response.result.role == "legrafica" ||
            response.result.role == "admin"
          ) {
            let isAdmin = userService.isAdmin(response.result);

            if (isAdmin.admin == true) {
              // para el administrador
              this.$router.push("/auth").catch((err) => {});
            } else {
              this.wait();
            }
          } else {
            this.$router.push("/").catch((err) => {});
          }
        } else {
          this.status = "error";
          this.message = response.message;
          this.delStatus();
          this.wait();
        }
      } else {
        this.status = "error";
        this.message = result.message;
        this.delStatus();
      }
    },
    toCheckout: async function () {
      await this.obtenerCarritos();
      let payload = {
        carrito: this.carrito,
      };
      let result = await this.$store.dispatch("carrito/validateCrt", {
        option: "valid_cart",
        item: payload,
      });

      if (result.status == "error") {
        this.status = "error";
        this.message = result.message; // result.message;
      } else {
        // success
        //si todo esta correcto redireccionar.
        return this.$router.push("/check-out").catch((err) => {});
      }
    },
    Add: function () {
      this.status = "";
      this.message = "";
      this.name = "";
      this.lastname = "";
      this.role = "cliente";

      this.phone = "";
      this.email = "";
      this.pass = "";
      this.passc = "";
      this.terms = false
      this.setAddedUsr("");
    },
  },
};
</script>
<style scoped>
a,p{
    font-family: var(--font-titulo1);
}
.log-reg-cont {
  display: flex;
  justify-content: space-between;
  width: 86.198vw;
  padding-top: 15vw;
  margin: auto auto 5.833vw;
}
.registro,
.login {
  width: 42.031vw;
  height: 39.583vw;
  /*height: 47.583vw;*/ 
  display: flex;
  justify-content: center;
  align-items: center;
}
.contra-cont {
  display: flex;
  flex-direction: column;
}
.login { 
  background-color: transparent !important;
  border: 1.5px solid var(--co-menui);
  align-items: flex-start !important;
  padding-top: 2.708vw;
  height: auto !important;
}
.login .input-txt-lr {
  border: 1.5px solid var(--co-menui);
}
.registro-cont,
.login-cont {
  width: 35.781vw;
}
.grid-flex {
  display: flex;
  justify-content: space-between;
}
.LogReg p.titulo-lr {
  margin: 0;
  font-family: var(--font-titulo1);
  font-weight: 400;
  font-size: 1.563vw;
  line-height: 1.979vw;
  color: #ff4713;
}
.LogReg p.titulo-lr.due {
  font-size: 1.042vw;
}
.LogReg a {
  color: #ff4713;
  text-decoration-color: transparent;
}
.LogReg p,
.LogReg label {
  font-family: var(--font-titulo1);
  font-style: normal;
  font-weight: 400;
  font-size: 0.833vw;
  line-height: 194.5%;
  color: #929292;
  margin: 0;
}
.LogReg label {
  font-size: 0.729vw;
  font-weight: 700;
}
.btn-lr {
  margin-top: 2.083vw;
  margin-bottom: 2.135vw;
}
.grid-inputs {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
.m-btm {
  margin-top: 1.302vw;
}
.input-lr-c {
  display: flex;
  flex-direction: column;
}
.grid-inputs .input-lr-c {
  margin-bottom: 1.771vw;
}
.input-txt-lr {
  width: 16.719vw;
  height: 1.979vw;
  border: 0.063vw solid var(--co-menui);
  border-radius: 0.359vw;
  background-color: transparent;
}
.acepts-adv input {
  width: 0.833vw;
  height: 0.833vw;
}
.btn-lr {
  width: 15.573vw;
  height: 3.906vw;
  border: 1px solid transparent;
  background-color: #ff4713;
  font-family: var(--font-titulo1);
  font-style: normal;
  font-weight: 400;
  font-size: 0.833vw;
  line-height: 2.031vw;
  color: #ffffff; 
  cursor: pointer;
  transition: 0.5s;
}
.input-txt-lr:focus {
  border: 1px solid #ff4713;
  color: #ff4713;
  font-weight: 700;
}
.login form{
  margin-top: 1vw;
}
.login .btn-lr {
  background-position-x: 12.302vw;
}
.btn-lr:hover {
  background-color: #bf6b1c;
}
.sm-reg-cont {
  margin: 0.667vw 0 0;
  padding-bottom: 1.667vw;
  height: 4.5vw;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.sm-reg-btn {
  font-family: "Poppins";
  font-style: normal;
  font-weight: 500;
  font-size: 0.729vw;
  line-height: 1.094vw;
  color: #686868;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 17.031vw;
  height: 1.979vw;
  background: #ffffff;
  border: 1.33188px solid #f0f0f0;
  border-radius: 10.655px;
  cursor: pointer;
  transition: 0.5s;
}
.sm-reg-btn:hover {
  background: #dedede;
}
.sm-reg-btn .icon {
  width: 0.763vw;
  height: 0.763vw;
  padding-right: 0.5vw;
}

@media (max-width: 768px) {
  .log-reg-cont {
    flex-direction: column;
  }
  .registro,
  .login {
    width: 100%;
    height: auto;
  }
  .registro {
    margin-bottom: 5.374vw;
  }
  .log-reg-cont {
    width: 94.393vw;
    padding-top: 25vw;
    margin: auto auto 5.833vw;
  }
  .LogReg p.titulo-lr {
    font-size: 7.009vw;
    line-height: 8.879vw;
  }
  .registro-cont,
  .login-cont {
    width: 80.841vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 11.215vw 0 16.589vw;
  }
  p.ryobe {
    width: 45vw;
    margin-bottom: 5.607vw;
  }
  .LogReg label {
    margin-bottom: 1.168vw;
  }
  .sm-reg-cont {
    margin: 4.673vw 0 0;
    padding-bottom: 1.667vw;
    height: 35.748vw;
  }
  .LogReg p,
  .LogReg label {
    font-size: 4.673vw;
    line-height: 118%;
    text-align: center;
  }
  .acepts-adv input {
    width: 7.009vw;
    height: 7.009vw;
  }
  .acepts-adv {
    margin-top: 8.645vw;
    display: flex;
  }
  .acepts-adv label {
    width: 67.523vw;
    text-align: left;
    margin-left: 6.075vw;
  }
  .grid-inputs {
    flex-direction: column;
    align-items: center;
  }
  .input-txt-lr {
    font-size: 4vw;
    width: 80.841vw;
    height: 18.925vw;
  }
  .input-lr-c {
    width: 100%;
    margin-top: 7.944vw;
  }
  .btn-lr {
    width: 100%;
    height: 17.991vw;
    font-size: 4.673vw;
    line-height: 9.112vw;
    margin: 8.178vw 0;
    background-size: 4.573vw;
    background-position-x: 58.302vw;
  }
  .grid-flex {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
  }
  /*.grid-inputs .input-lr-c {
    margin-bottom: 8.645vw;
}*/
  .LogReg p.titulo-lr.due {
    font-size: 5.607vw;
  }
  .sm-reg-btn {
    width: 80.841vw;
    height: 16.355vw;
    font-size: 4.673vw;
  }
  .sm-reg-btn .icon {
    width: 3.423vw;
    height: 3.423vw;
    padding-right: 2.5vw;
  }
  .login {
    background-position-x: 6.075vw;
    background-position-y: 171.262vw;
    background-size: 81.776vw;
  }
  .login-cont {
    padding: 11.215vw 0 79.589vw;
  }
}
</style>