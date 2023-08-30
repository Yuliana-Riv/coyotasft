<template>
  <div id="AddPrd">
    <div class="form-content">
      <form>
        <section v-if="added !== ''">
          <div class="grup-form"> 
            <p class="add_it">Nombre: <span>{{ added.name }}</span></p>
            <p class="add_it">Descripción: <span>{{ added.descr }}</span></p>
            <p class="add_it">Categoría: <span>{{ added.category_name }}</span></p> 
            <img
              class="img_item"
              v-if="added.image !== ''" 
              :src="urlr + '/' + endpointCodes.get + '/product-img/' + added.image"
              alt=""
            />
          </div>
          <hr class="hrdr" />          
        </section>


        
        <div class="grup-form dflx" v-if="added == ''">
          <!--nombre-->
          <div class="boxform">
            <label for="name" class="name">Nombre </label>
            <input
              v-model="name"
              type="text"
              id="name"
              name="name"
              required
              class="in1"
            />
          </div>
        </div>

        <div class="grup-form dflx" v-if="added == ''">
          <!--descripcion-->
          <div class="boxform">
            <label for="descr" class="descr"
              >Descripción <span class="opcional">(opcional)</span></label
            >
            <textarea v-model="descr" id="descr" name="descr" class="in1" />
          </div>
        </div>

        <div class="grup-form dflx" v-if="added == ''">
          <!--categoría-->
          <div class="boxform">
            <label for="category" class="role">Categoría</label>

            <input
              v-model="cat_name"
              type="text"
              id="category"
              name="category"
              disabled
              required
            />

            <div class="content-tbl-items">
              <div class="tblitems">
                <div class="bodytbl-items tbl_item">
                  <div v-if="categorias.length > 0">
                    <div v-for="(prm, key) in categorias" :key="key">
                      <p
                        v-if="includesItem(value1, prm.name)"
                        class="itemp cp"
                        @click="(cat_name = prm.name), (id_category = prm.id)"
                      >
                        {{ prm.name }}
                      </p>
                    </div>
                  </div>
                  <div v-else>
                    <p class="item cp">No se encontraron coincidencias.</p>
                  </div>
                </div>
              </div>
              <div class="buscador-items dflx">
                <input
                  v-model="value1"
                  type="search"
                  id="inputbusqueda"
                  class="form-control searching-it"
                  :placeholder="'Búsqueda'"
                />
                <div class="icon_buscar">
                  <img
                    src="../../assets/default/Search.png"
                    alt="icono buscar"
                  />
                </div>
              </div>
            </div>
          </div>

          <!--type-->
          <!-- <div class="boxform">
            <label for="role" class="role">Presentación</label>

            <input
              v-model="type_name"
              type="text"
              id="tipos"
              name="tipos"
              disabled
              required
            />

            <div class="content-tbl-items">
              <div class="tblitems">
                <div class="bodytbl-items tbl_item">
                  <div
                    v-if="
                      type.length>0
                    "
                  >
                    <div v-for="(prm, key) in type" :key="key">
                      <p
                        v-if="includesItem2(value2, prm.name)"
                        class="itemp cp"
                        @click="(type_name = prm.name), (id_type = prm.id)"
                      >
                        {{ prm.name }}
                      </p>
                    </div>
                  </div>
                  <div v-else>
                    <p class="item cp">No se encontraron coincidencias.</p>
                  </div>
                </div>
              </div>
              <div class="buscador-items dflx">
                <input
                  v-model="value2"
                  type="search"
                  id="inputbusqueda"
                  class="form-control searching-it"
                  :placeholder="'Búsqueda'"
                />
                <div class="icon_buscar">
                  <img src="../../assets/default/Search.png" alt="icono buscar" />
                </div>
              </div>
            </div>
          </div> -->
        </div>
        <div class="grup-form dflx" v-if="added == ''">
          <div class="boxform">
            <label for="role" class="role"
              >Agregar variates del producto
            </label>
            <div class="two-options">
              <div class="dflx">
                <div
                  class="to-btn"
                  @click="more_pro = 'SI'"
                  :class="{ active: more_pro == 'SI' }"
                >
                  CON VARIANTES
                </div>
                <div
                  class="to-btn"
                  @click="more_pro = 'NO'"
                  :class="{ active: more_pro == 'NO' }"
                >
                  SIN VARIANTE
                </div>
              </div>
            </div>
            <label for="role" class="role adv2" v-if="more_pro == 'SI'">
              **Agregar precio al momento de añadir atributo.
            </label>
          </div>
        </div>

        <div class="grup-form dflx">
          <!--precio-->
          <div class="boxform" v-if="(added == '' ? more_pro == 'NO' : added.more_pro == 'NO')">
            <label for="price" class="price">Precio </label>
            <input
              v-model="price"
              type="number"
              id="price"
              name="price"
              min="1"
              step="any"
              required
              class="in1"
            />
          </div>

          <div class="boxform"  v-if="(added == '' ? added == '' : added.more_pro == 'NO')">
            <label>Imagen <span class="opcional">(opcional)</span></label>
            <div class="dflx">
              <label class="filelabel" for="uploadimg">
                <span>Seleccionar Archivo</span></label
              >
              <label class="filelabelname tbl_item" for="uploadimg">
                {{ archivo }}</label
              >
            </div>

            <input
              @change="previewFiles"
              type="file"
              id="uploadimg"
              name="uploadimg"
            />
          </div>
        </div>

        <div>
          <hr class="hrdr" />
          <p class="subtitle">
            Subcategoría <span class="opcional">(opcional)</span>
          </p>

          <form @submit.prevent="addSubcategory(itemsub)">
            <div class="grup-form dflx">
              <!--categoría-->
              <div class="boxform">
                <label for="category" class="category">Seleccionada</label>

                <input
                  v-model="sub_name"
                  type="text"
                  id="category"
                  name="category"
                  disabled
                  required
                />

                <div class="content-tbl-items">
                  <div class="tblitems">
                    <div class="bodytbl-items tbl_item">
                      <div v-if="subcategorias.length > 0">
                        <div v-for="(prm, key) in subcategorias" :key="key">
                          <p
                            v-if="includesItem(value3, prm.name)"
                            class="itemp cp"
                            @click="
                              (sub_name = prm.name),
                                (id_subcategory = prm.id),
                                (itemsub = prm)
                            "
                          >
                            <!--parent_cat_name-->
                            {{ prm.name }}
                          </p>
                        </div>
                      </div>
                      <div v-else>
                        <p class="item cp">No se encontraron coincidencias.</p>
                      </div>
                    </div>
                  </div>
                  <div class="buscador-items dflx">
                    <input
                      v-model="value3"
                      type="search"
                      id="inputbusqueda"
                      class="form-control searching-it"
                      :placeholder="'Búsqueda'"
                    />
                    <div class="icon_buscar">
                      <img
                        src="../../assets/default/Search.png"
                        alt="icono buscar"
                      />
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="dflx">
              <button class="alta" type="submit">Agregar</button>
            </div>
          </form>

          <div class="tabla_perzonalidada">
            <div class="header_tp">
              <p class="op_tp">Subcategoría</p>
              <p class="op_tp">Categoría</p>
              <p class="op_del_tb">Eliminar</p>
            </div>
            <div class="body_tp">
              <div class="fila" v-for="(item, key) in subcat" :key="key">
                <p class="fp_tp">{{ item.name }}</p>
                <p class="fp_tp">{{ item.category_name }}</p>
                <p @click="subcat = []" class="fdel">&#10006;</p>
              </div>
              <div class="sinitems" v-if="subcat.length == 0">
                <p>Sin subcategoría agregada</p>
              </div>
            </div>
          </div>
        </div>

        <!--<hr class="hrdr" />
        <p class="subtitle">Extras <span class="opcional">(opcional)</span></p>

        <form @submit.prevent="addExtra(price_ext, descr_ext)">
          <div class="grup-form dflx"> 
            <div class="boxform">
              <label for="price_ext" class="price">Precio </label>
              <input
                v-model="price_ext"
                type="number"
                id="price_ext"
                name="price_ext"
                min="1"
                step="any"
                required
                class="in1"
              />
            </div>
          </div>
          <div class="grup-form dflx"> 
            <div class="boxform">
              <label for="descr_ext" class="descr">Descripción</label>
              <textarea
                v-model="descr_ext"
                id="descr"
                name="descr_ext"
                required
                class="in1"
              />
            </div>
          </div>

          <div class="dflx">
            <button class="alta" type="submit">Aceptar</button>
          </div>
        </form>

        <div class="tabla_perzonalidada">
          <div class="header_tp">
            <p class="op_tp">Descripción</p>
            <p class="op_tp">Precio</p>
            <p class="op_del_tb">Eliminar</p>
          </div>
          <div class="body_tp">
            <div class="fila" v-for="(item, key) in extras" :key="key">
              <p class="fp_tp">{{ item.descr }}</p>
              <p class="fp_tp">${{ item.price }}</p>
              <p @click="delExtra(key)" class="fdel">&#10006;</p>
            </div>
            <div class="sinitems" v-if="extras.length == 0">
              <p>Sin extras agregados</p>
            </div>
          </div>
        </div>-->

        <!--regresar/guardar-->
        <div class="dflx reg_gu_cont">
          <p @click="wait()" class="btnRegresar">Regresar</p>
          <!--guardar primer producto-->
          <div
            class="alta"
            @click="
              submit(
                name,
                id_category,
                descr,
                price,
                file1,
                extras,
                subcat,
                more_pro
              )
            "
            v-if="added == ''"
          >
            Guardar
          </div>
          <!--guardar otro producto-->
          <div
            class="alta"
            @click="
              submit(
                added.name,
                added.id_category,
                added.descr,
                price,
                file1,
                extras,
                subcat,
                added.more_pro
              )
            "
            v-else
          >
            Guardar
          </div>
        </div>

        <div v-if="status != ''" class="status_messages">
          <div v-if="status == 'success'" class="msg msg_success">
            <p>{{ message }}</p>
          </div>
          <div v-if="status == 'error'" class="msg msg_error">
            <p>{{ message }}</p>
          </div>
        </div>
      </form>

      <div v-if="viewModal" class="modal_view">
        <div id="modal_add">
          <div class="body dflx">
            <h3>
              Producto agregado con éxito. <br /><br />
              <span>
                Haz click en <b>continuar</b> para agregar <b><span v-if="more_pro == 'SI'">atributo, </span>precio y stock.</b>
              </span>
            </h3>
            <img src="../../assets/default/add.png" alt="icono alerta" />
          </div>

          <div class="modal_add_btns dflx">
            <!--<p @click="Add()" class="otro">Aceptar</p>-->
            <p @click="toEdit()" class="editar">Continuar</p>
            <p @click="back()" class="inicio">Regresar</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { mapActions } from "vuex";
let { url, endpointCodes } = require("../../global/index");
export default {
  name: "AddPrd",
  data() {
    return {
      urlr: url,
      endpointCodes: endpointCodes,
      status: "",
      message: "",

      name: "",
      descr: "",
      id_category: "",
      id_type: "",
      price: "",
      more_pro: "NO",

      cat_name: "NINGUNA",
      type_name: "NINGUNA",

      sub_name: "NINGUNA",
      id_subcategory: "",
      subcat: [],
      itemsub: "",

      url: "",

      search_value: "",
      updsearchcli: "",

      price_ext: "",
      descr_ext: "",
      extras: [],

      active: false,
      active2: false,
      value1: "",
      value2: "",
      value3: "",
      archivo: "No se eligió archivo",
      file1: null,

      //MODAL

      viewModal: false,
    };
  },
  created() {
    this.getAllInfoCtg("category");
    //this.getAllInfoTpe("type");
  },
  watch: {
    id_category: async function (value) {
      this.subcat = [];
      if (value) {
        const payload2 = {
          id: value,
          option: "category_subcategory",
        };
        await this.getInfoByIdSct(payload2);
      }
    },
  },

  computed: {
    added() {
      return this.$store.getters["product/getAdded"];
    },
    categorias() {
      let arr = this.$store.getters["category/data"];
      if (Array.isArray(arr)) {
        return arr;
      } else {
        return [];
      }
    },
    subcategorias() {
      let arr = this.$store.getters["subcategory/data"];
      if (Array.isArray(arr)) {
        return arr;
      } else {
        return [];
      }
    },
    /*type() {
      let arr =  this.$store.getters["type/data"];
       if(Array.isArray(arr)){
        return arr
      }else{
        return []
      }
    },*/
  },
  methods: {
    ...mapActions("product", ["getAllInfoPrd"]),
    ...mapActions("product", ["setAddedPrd"]),
    ...mapActions("product", ["setHistoryOptionPrd"]),
    ...mapActions("product", ["getInfoByIdPrd"]),
    ...mapActions("category", ["getAllInfoCtg"]),
    ...mapActions("category", ["setAddedCtg"]),
    ...mapActions("category", ["setHistoryOptionCtg"]),
    ...mapActions("type", ["getAllInfoTpe"]),
    ...mapActions("type", ["setAddedTpe"]),
    ...mapActions("type", ["setHistoryOptionTpe"]),
    ...mapActions("subcategory", ["getInfoByIdSct"]),
    wait: function () {
      setTimeout(() => this.$router.go(), 200);
    },
    addSubcategory(item) {
      this.subcat = [item];
      this.itemsub = "";
      this.sub_name = "NINGUNA";
      this.id_subcategory = "";
    },
    submit: async function (
      name,
      id_category,
      descr,
      price,
      image,
      extras,
      subcat,
      more_pro
    ) {
      this.status = "";
      this.message = "";
      let data = [];
      extras = JSON.stringify(extras);
      subcat = JSON.stringify(subcat);
      let p = price;
      if(more_pro == 'SI'){
        p = 1
      }
      if (image == null) {
        data = {
          name: name,
          id_category: id_category, 
          descr: descr,
          price: p,
          extras,
          subcat,
          more_pro,
        };
      } else {
        data = new FormData();
        data.append("name", name);
        data.append("id_category", id_category);

        data.append("descr", descr);
        data.append("price", p);
        data.append("image", image);
        data.append("subcat", subcat);

        data.append("extras", extras);
        data.append("more_pro", more_pro);
        data.append("_method", "POST");
      }
      let result = await this.$store.dispatch("product/addItemPrd", {
        option: "product",
        item: data,
      });
      console.log(result);

      if (result.status == "error") {
        this.status = "error";
        this.message = result.message;
      } else {
        // success
        let payload = {
          id: result.added.id,
          option: "product",
        };
        let arrl = await this.getInfoByIdPrd(payload);
        this.setAddedPrd(arrl);
        /**/
        if (arrl.more_pro == true) {
          this.active2 = true;
        }
        this.showModal();
      }
    },
    closeSelect() {
      this.active = false;
      document.getElementById("select-ch").checked = false;
    },
/* 
    addExtra(price, descr) {
      let arr = [];
      for (const item of this.extras) {
        arr.push(item);
      }
      arr.push({
        price,
        descr,
      });
      this.extras = arr;
    },
    delExtra(indice) {
      let arr = [];
      for (var i = 0; i < this.extras.length; i++) {
        if (i != indice) {
          arr.push(this.extras[i]);
        }
      }
      this.extras = arr;
    },*/

    includesItem(search, name) {
      if (search == "") {
        return true;
      }
      name = name.toLowerCase();
      search = search.toLowerCase();
      if (search == "") {
        return false;
      }
      return name.includes(search);
    },

    includesItem2(search, name) {
      if (search == "") {
        return true;
      }
      name = name.toLowerCase();
      search = search.toLowerCase();
      if (search == "") {
        return false;
      }
      return name.includes(search);
    },

    showModal: function () {
      this.viewModal = true;
    },
    closeModal: function () {
      this.viewModal = false;
      this.setAddedPrd("");
      this.setHistoryOptionPrd("Default");
    },
    Add: function () {
      this.status = "";
      this.message = "";
      this.name = "";

      this.id_category = "";
      this.id_type = "";
      this.cat_name = "NINGUNA";
      this.type_name = "NINGUNA";
      this.descr = "";

      this.price = "";

      this.file1 = null;

      this.viewModal = false;
      this.setAddedPrd("");
    },
    toEdit: function () {
      this.setHistoryOptionPrd("Edit");
      this.viewModal = false;
    },
    back: function () {
      setTimeout(() => this.$router.go(), 200);
    },
    previewFiles(e) {
      var files = e.target.files || e.dataTransfer.files;
      if (!files.length) return;
      this.file1 = files[0];
      this.archivo = this.file1.name;
    },
  },
};
</script>
<style scoped>
.grup-form {
  align-items: flex-start;
}
#AddPrd label {
  color: var(--color-2);
  font-weight: 700;
  font-size: 0.7291666666666666vw;
  margin-bottom: 0.3vw;
}
#AddPrd label.adv2{ 
  color: #afafaf;
  margin: 1vw 0 2.3vw;
}
#AddPrd input,
#AddPrd select {
  height: 2.5vw;
  width: 14.716666666666668vw;
  border: 0.052083vw solid var(--color-2);
  border-radius: 0vw 1.5vw 1.5vw 0vw;
  color: var(--color-4);
  font-size: 0.7291666666666666vw;
  font-weight: 500;
  padding-left: 1.09375vw;
}

#select-role {
  height: 2.5vw;
  width: 13.716667vw;
  border: 0.052083vw solid var(--color-2);
  border-radius: 0vw 1.5vw 1.5vw 0vw;
  color: var(--color-4);
  font-size: 0.7291666666666666vw;
  font-weight: 500;
  padding-left: 1.09375vw;
  display: flex;
  align-items: center;
  background-image: url("../../assets/default/blueflecha.svg");
  background-repeat: no-repeat;
  background-position-y: center;
  background-position-x: 12.6vw;
}
#select-role.rounded {
  border-radius: 0vw 1.5vw 0vw 0vw;
  border-left: 0.052083vw solid var(--color-2);
  border-right: 0.052083vw solid var(--color-2);
  border-top: 0.052083vw solid var(--color-2);
  border-bottom: 0;
}
#select-ch:checked ~ .options-cont {
  display: flex;
  position: absolute;
  padding: 0.573vw 1.25vw;
  flex-direction: column;
  background-color: white;
  width: 12.3vw;
  border-left: 0.052083vw solid var(--color-2);
  border-right: 0.052083vw solid var(--color-2);
  border-top: 0;
  border-bottom: 0.052083vw solid var(--color-2);
}
#modal_add .body {
  height: 6.395833vw !important;
}
#modal_add img {
  padding-top: 2.54vw !important;
  padding-left: 1vw !important;
}
#modal_add h3 {
  padding-top: 1.1177083vw !important;
  width: 12vw !important;
}
p.add_it {
    color: var(--color-2);
    font-weight: 700;
    font-size: 0.7291666666666666vw;
    margin-bottom: 0.3vw;
}
p.add_it span {
    color: silver;
}
img.img_item{
  margin-top: 1vw;
    border-radius: 1.2vw;
}
</style>
