<template>
  <div
    class="Navigator"
    :class="{ adjust: scrollP > 0, azul: $route.name == '404' }"
  >
    <div class="nav-cont" :class="{ pdd: scrollP > 0 }">
      <!--<img :src="pcLogo" alt="logo" class="logo pc" :class="{'logodis':scrollP > 0}"/>
      <img :src="moLogoHor" alt="logo" class="logo pc" :class="{'hht':scrollP > 0,'logodis':scrollP < 400}"/>-->
      <a href="/"
        ><div
          class="logo"
          :class="{ hht: scrollP > 0, logodis: scrollP > 0 }"
        ></div
      ></a>
      <img
        src="../assets/custom/bars.svg"
        alt=""
        class="bars mo"
        :class="{ filt: scrollP > 0 }"
        @click="open = true"
      />
      <div class="menu-cont" :class="{ activated: open }">
        <img
          src="../assets/custom/cross.svg"
          alt=""
          class="bars mo"
          @click="open = false"
        />

        <a href="/" class="menu-a first active">INICIO</a>
        <p @click="locate('nosotros')" class="menu-a">NOSOTROS</p>
        <p @click="locate('menu')" class="menu-a">MENÚ</p>
        <p @click="locate('contacto')" class="menu-a">CONTACTO</p>
        <a href="/carrito" @click="open = false" class="menu-a cart">CARRITO</a>
        <!--<a href="#sucursales" @click="open = false" class="menu-a">SUCURSALES</a>-->
        <div class="search-cont" v-if="buscador">
          <button><img src="../assets/lupa.svg" alt="" class="lupa" /></button>
          <input type="search" id="site-search" name="q" />
        </div>
        <!--  -->
        <div class="sm-cont">
          <a
            href="https://www.facebook.com/people/Coyotas-Lourdes-Hermosillo/100042529255381/"
            target="_blank"
            rel="noopener noreferrer"
          >
            <img
              src="../assets/custom/fb-i.svg"
              alt="sm"
              class="sm-i"
              :class="{ ylw: scrollP > 0 || $route.name == '404' }"
            />
          </a>
          <a
            href="https://www.instagram.com/lourdescoyotas"
            target="_blank"
            rel="noopener noreferrer"
          >
            <img
              src="../assets/custom/ig-i.svg"
              alt="sm"
              class="sm-i"
              :class="{ ylw: scrollP > 0 || $route.name == '404' }"
            />
          </a>
          <a
            href="https://www.tiktok.com/@lourdescoyotas"
            target="_blank"
            rel="noopener noreferrer"
          >
            <img
              src="../assets/custom/tt-i.svg"
              alt="sm"
              class="sm-i"
              :class="{ ylw: scrollP > 0 || $route.name == '404' }"
            /> </a
          ><!---->
        </div>
        <div class="user-bar">
          <a href="/carrito">
            <img src="../assets/custom/cart1.svg" alt="sm" class="cart" />
          </a>
          <a href="/" class="c-div" v-if="identity.role == 'cliente'">
            <img src="../assets/custom/user1.svg" alt="sm" class="user" />
            <span>¡Hola! {{ identity.fullname }}</span>
          </a>
          <a
            href="/administrador"
            class="c-div"
            v-else-if="identity.role == 'admin'"
          >
            <img src="../assets/custom/user1.svg" alt="sm" class="user" />
            <span>¡Hola! {{ identity.fullname }}</span>
          </a>
          <a
            href="/administrador"
            class="c-div"
            v-else-if="identity.role == 'legrafica'"
          >
            <img src="../assets/custom/user1.svg" alt="sm" class="user" />
            <span>¡Hola! {{ identity.fullname }}</span>
          </a>
          <a href="/login" class="c-div" v-else>
            <img src="../assets/custom/user1.svg" alt="sm" class="user" />
            <span class="mo">Inicia sesión</span>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import pcLogo from "../assets/logonav.png";
import moLogo from "../assets/logonav-mo.png";
import moLogoHor from "../assets/logosticky.png";
export default {
  data() {
    return {
      buscador: true /* Activar buscador */,
      moLogo,
      pcLogo,
      moLogoHor,
      open: false,
      scrollP: localStorage.getItem("scroll"),
    };
  },
  async created() {
    await this.getIdentity();
  },
  computed: {
    identity() {
      return this.$store.getters["admin/getIdentity"];
    },
  },
  methods: {
    scroll(event) {
      let number = event.target.documentElement.scrollTop;
      let offset = number * 1;
      localStorage.setItem("scroll", offset);
      this.scrollP = localStorage.getItem("scroll");
    },
    getIdentity: async function () {
      let response = await this.$store.dispatch("admin/getData");
      return response;
    },
    locate(val) {
      let min768 = window.matchMedia("(min-width: 768px)");
      let media768 = window.matchMedia("(max-width: 768px)");
      localStorage.setItem("navop", val);
      let rute = localStorage.getItem("navop");
      this.open = false;
      if (this.$route.name == "Home") {
        window.location.href = "/#" + val;
      } else {
        if (media768.matches) {
          if (rute == "nosotros") {
            this.$router.push("/#" + val).catch((err) => {});
            setTimeout(() => {
            window.scrollTo(0, 621);
            }, 1000);

          }
          if (rute == "menu") {
            this.$router.push("/#" + val).catch((err) => {});
            setTimeout(() => {
            window.scrollTo(0, 1621);
            }, 1000);

          }
          if (rute == "contacto") {
            this.$router.push("/#" + val).catch((err) => {});
            setTimeout(() => {
            window.scrollTo(0, 6251);
            }, 1000);

          }
        } else if (min768.matches) {
          if (rute == "nosotros") {
            this.$router.push("/#" + val).catch((err) => {});
            setTimeout(() => {
              window.scrollTo(0, 712);
            }, 1000);
          }
          if (rute == "menu") {
            this.$router.push("/#" + val).catch((err) => {});
            setTimeout(() => {
              window.scrollTo(0, 1321.5999755859375);
            }, 1000);
          }
          if (rute == "contacto") {
            setTimeout(() => {
              window.scrollTo(0, 5000.7998046875);
            }, 1000);
            this.$router.push("/#" + val).catch((err) => {});
          }
        }
      }
    },
  },
  mounted() {
    window.addEventListener("scroll", this.scroll);
  },
};
</script>
<style scoped>
.pc {
  display: block;
}
.mo {
  display: none;
}
.Navigator {
  transition: 0.5s;
  width: 100%;
  position: fixed;
  z-index: 1300;
}
.nav-cont {
  transition: 0.5s;
  width: 88.698vw;
  margin: 0 auto;
  padding: 2.796vw 0 2.344vw;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.Navigator .logo {
  width: auto;
  height: 8.021vw;
  transition: 0.65s;
}
.menu-cont {
  display: flex;
  align-items: center;
}
/**items menu */
.Navigator.azul .menu-a {
  color: #005cb9;
}
.menu-a {
  font-family: var(--font-titulo1);
  font-size: var(--fs-menupc);
  color: var(--co-menui);
  margin: 0 1.25vw;
  transition: 0.5s;
  cursor: pointer;
}
.menu-a:hover {
  color: var(--co-menui-active);
  font-weight: 700;
}
/**buscador */
.search-cont {
  width: 8.542vw;
  height: 1.771vw;
  display: flex;
  align-items: center;
  border: var(--im-border);
  border-radius: 1.563vw;
}
.search-cont button {
  background: none;
  border: none;
  padding: 0;
  width: 1.785vw;
}
.search-cont button img {
  width: 0.885vw;
  background: none;
  border: none;
  margin-left: 0.732vw;
  display: flex;
  filter: var(--lupapc-color);
}
.search-cont input#site-search {
  width: 100%;
  height: auto;
  background: none;
  border: none;
  font-family: var(--font-titulo2);
  font-size: var(--fs-menupc);
  color: var(--co-menui);
}

/**social media cont */
.sm-cont {
  /* width: 4.917vw;*/
  width: 5.469vw;
  height: 1.406vw;
  margin-left: 0.886vw;
  display: flex;
  justify-content: space-between;
}
.sm-cont a {
  display: flex;
}
.sm-cont img {
  width: 1.354vw;
  filter: invert(49%) sepia(88%) saturate(4962%) hue-rotate(351deg)
    brightness(99%) contrast(104%);
}
.sm-cont img.ylw {
  filter: var(--sm-icon-color);
}
.sm-cont img:hover {
  filter: var(--sm-icon-hover);
}
.adjust {
  background-color: var(--fondo-menufijo);
}
.adjust .menu-a {
  color: var(--co-txtmefi);
}
.adjust .menu-a:hover {
  color: var(--co-menui-active);
}
@media (min-width: 768px) {
  .menu-a.cart {
    display: none;
  }
  .hht {
    height: 4.221vw !important;
  }
  .pdd {
    padding: 0.4vw 0 0.4vw !important;
  }
  .Navigator .logo {
    background-image: url("../assets/logonav.png");
    background-size: 100%;
    background-repeat: no-repeat;
    background-position: center;
    width: 21.458vw;
  }
  .logodis {
    background-image: url("../assets/logosticky.png") !important;
    width: 10.122396vw !important;
  }
  .user-bar {
    display: flex;
    margin-left: 2.708vw;
  }
  .user-bar .c-div {
    display: flex;
    align-items: center;
    margin-left: 0.99vw;
  }
  .user-bar .c-div span {
    font-size: 0.625vw;
    line-height: 0.781vw;
    margin-left: 0.729vw;
    color: var(--co-menui);
    font-family: var(--Inter);
    font-weight: 700;
  }
  .user-bar .cart {
    width: 1.667vw;
  }
  .user-bar .user {
    width: 1.094vw;
  }
  .user-bar .c-div span.mo {
    display: none;
  }
}
/**MOBILE STYLES */
@media (max-width: 768px) {
  .user-bar .c-div span.mo {
    display: block;
  }
  .menu-a.cart {
    display: block;
  }
  .user-bar .cart {
    display: none;
  }
  .user-bar .user {
    width: 7.246vw;
  }
  .Navigator .logo {
    background-image: url("../assets/logonav.png");
    background-size: 100%;
    background-repeat: no-repeat;
    background-position: center;
    width: 42.995vw;
    height: 16.021vw !important;
  }
  .logodis {
    background-image: url("../assets/logosticky.png") !important;
    width: 42.995vw !important;
    height: 16.021vw !important;
  }
  .pc {
    display: none;
  }
  .mo {
    display: block;
  }
  .bars {
    width: 10.628vw;
    filter: var(--menu-bars);
  }
  .bars.filt {
    filter: invert(81%) sepia(46%) saturate(1024%) hue-rotate(352deg)
      brightness(101%) contrast(99%);
  }
  .activated {
    display: flex !important;
  }
  .activated .bars {
    filter: var(--co-menui-mo);
  }
  .activated .sm-cont img {
    filter: var(--co-menuism-mo);
  }
  .activated .bars {
    width: 7.488vw;
  }
  .activated .sm-cont img {
    width: 14.251vw;
  }
  .menu-cont {
    display: none;
    position: fixed;
    background: var(--fondo-bk);
    top: 0;
    right: 0;
    width: 54.831vw;
    height: 100%;
    z-index: 100;
    flex-direction: column;
    align-items: flex-end;
    overflow-y: scroll;
    padding: 10.386vw 7.971vw 10.386vw 14.493vw;
  }
  .nav-cont {
    width: 86.715vw;
    margin: 0 auto;
    padding: 4.106vw 0 4.831vw;
  }
  .menu-a {
    font-family: var(--font-titulo1);
    font-size: var(--fs-menumo);
    color: #005cb9 !important;
    font-weight: 500;
    margin: 0 0 5.556vw;
    transition: 0.5s;
    text-align: right;
    letter-spacing: 0.5vw;
  }
  .menu-a.first {
    margin: 18.841vw 0 4.71vw !important;
  }
  .divlogo {
    display: none;
  }
  /*.Navigator .logo {
    width: auto;
    height: 23.430vw;
  }*/
  .hht {
    height: 16.184vw !important;
  }
  .search-cont {
    width: 54.831vw;
    height: 16.908vw;
    border-radius: 7.246vw;
    border: var(--im-border-mo);
    margin-top: 11.836vw;
  }
  .search-cont button {
    width: 15.744vw;
  }
  .search-cont button img {
    width: 8.744vw;
    margin-left: 6.498vw;
    filter: var(--lupamo-color);
  }
  .search-cont input#site-search {
    font-family: var(--font-parrafo);
    font-size: var(--fs-menumo);
    color: var(--color-menumo);
  }
  .sm-cont {
    width: 54.831vw;
    height: 13.527vw;
    margin-top: 7.488vw;
    margin-bottom: 14.251vw;
    margin-left: 0.886vw;
    display: flex;
    justify-content: space-between;
  }
  .sm-cont img {
    width: 14.251vw;
  }
  .user-bar span {
    font-weight: 700;
    font-size: 3.623vw;
    line-height: 4.348vw;
    letter-spacing: 0.3vw;
    color: var(--co-userbartxt);
    padding-left: 3.865vw;
  }
  .user-bar .c-div {
    display: flex;
    align-items: center;
    width: 56vw;
  }
}
</style>
