<template>
  <div>
    <div id="detail">
      <Navbar />
    </div>
    <!-- Button trigger modal -->

    <!-- Modal -->
    <div
      class="modal fade"
      id="exampleModal"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="exampleModalLabel">
              Form<span v-show="!updateSubmitJabar"> Tambah</span
              ><span v-show="updateSubmitJabar"> Update</span>
            </h1>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
              @click="close"
            ></button>
          </div>
          <div class="modal-body"></div>
        </div>
      </div>
    </div>
    <table class="table table-dark table-hover">
      <thead>
        <tr>
          <th scope="col">No.</th>
          <th scope="col">Wisata</th>
          <th scope="col">Kota</th>
          <th scope="col">Tradisi</th>
          <th scope="col">Luas</th>
          <th scope="col">Monumen</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(jabar, index) in jabars" :key="jabar.id">
            <td>{{index + 1}}</td>
          <td>{{ jabar.wisjabar }}</td>
          <td>{{ jabar.kota }}</td>
          <td>{{ jabar.budayajabar }}</td>
          <td>{{ jabar.Transportasijabar }}</td>
          <td>
            <img :src="jabar.imagejabar" alt="" width="100" height="100" />
          </td>
        </tr>
      </tbody>
    </table>
    <!-- Table Jateng -->
    <!-- Button trigger modal -->

    <!-- Modal -->
    <div
      class="modal fade"
      id="jateng"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="exampleModalLabel">
              Form<span v-show="!updateSubmit"> Tambah</span
              ><span v-show="updateSubmit"> Update</span>
            </h1>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
              @click="close"
            ></button>
          </div>
          <div class="modal-body"></div>
        </div>
      </div>
    </div>
    <div>
      <table class="table table-dark table-hover">
        <thead>
          <tr>
            <th scope="col">No.</th>
            <th scope="col">Wisata</th>
            <th scope="col">Kota</th>
            <th scope="col">Tradisi</th>
            <th scope="col">Luas</th>
            <th scope="col">Monumen</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(jateng, index) in jatengs" :key="jateng.id">
            <td>{{index + 1}}</td>
            <td>{{ jateng.wisjateng }}</td>
            <td>{{ jateng.kotajateng }}</td>
            <td>{{ jateng.budayajateng }}</td>
            <td>{{ jateng.Transportasijateng }}</td>
            <td>
              <img :src="jateng.imagejateng" alt="" width="100" height="100" />
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import axios from "axios";
import Navbar from "../components/Navbar.vue";
export default {
  name: "HomeE",
  components: {
    Navbar,
  },
  data() {
    return {
      form: {
        id: "",
        wisjabar: "",
        kota: "",
        budayajabar: "",
        Transportasijabar: "",
        imagejabar: "",
      },
      jabars: "",
      updateSubmitJabar: false,

      form: {
        id: "",
        wisjateng: "",
        kotajateng: "",
        budayajateng: "",
        Transportasijateng: "",
        imagejateng: "",
      },
      jatengs: "",
      updateSubmitJateng: false,
    };
  },
  mounted() {
    if (!sessionStorage.getItem("USER_DATA")) {
      this.$router.push("/");
    }
    this.loadjabar();
    this.loadjateng();
  },
  methods: {
    loadjabar() {
      axios
        .get("http://localhost:3000/jabars")
        .then((res) => {
          this.jabars = res.data; //respon dari rest api dimasukan ke jabars
        })
        .catch((err) => {
          console.log(err);
        });
    },
    loadjateng() {
      axios
        .get("http://localhost:3000/jatengs")
        .then((res) => {
          this.jatengs = res.data; //respon dari rest api dimasukan ke jabars
        })
        .catch((err) => {
          console.log(err);
        });
    },
    addjabar() {
      axios
        .post("http://localhost:3000/jabars/", this.formjabar)
        .then((res) => {
          this.loadjabar();
          this.form.id = "";
          this.form.wisjabar = "";
          this.form.kota = "";
          this.form.budayajabar = "";
          this.form.Transportasijabar = "";
          this.form.imagejabar = "";
        });
    },
    addjateng() {
      axios.post("http://localhost:3000/jatengs/", this.form).then((res) => {
        this.loadjateng();
        this.form.id = "";
        this.form.wisjabar = "";
        this.form.kota = "";
        this.form.budayajabar = "";
        this.form.Transportasijabar = "";
        this.form.imagejabar = "";
      });
    },
    edit1(jabar) {
      this.updateSubmitJabar = true;
      this.form.id = jabar.id;
      this.form.wisjabar = jabar.wisjabar;
      this.form.kota = jabar.kota;
      this.form.budayajabar = jabar.budayajabar;
      this.form.Transportasijabar = jabar.Transportasijabar;
      this.form.imagejabar = jabar.imagejabar;
    },
    edit(jateng) {
      this.updateSubmit = true;
      this.form.id = jateng.id;
      this.form.wisjateng = jateng.wisjateng;
      this.form.kotajateng = jateng.kotajateng;
      this.form.budayajateng = jateng.budayajateng;
      this.form.Transportasijateng = jateng.Transportasijateng;
      this.form.imagejateng = jateng.imagejateng;
    },
    update(form) {
      return axios
        .put("http://localhost:3000/jabars/" + form.id, {
          wisjabar: this.form.wisjabar,
          kota: this.form.kota,
          budayajabar: this.form.budayajabar,
          Transportasijabar: this.form.Transportasijabar,
          imagejabar: this.form.imagejabar,
        })
        .then((res) => {
          this.loadjabar();
          this.form.id = "";
          this.form.wisjabar = "";
          this.form.kota = "";
          this.form.budayajabar = "";
          this.form.Transportasijabar = "";
          this.form.imagejabar = "";
          this.updateSubmitJabar = false;
        })
        .catch((err) => {
          console.log(err);
          return axios
            .put("http://localhost:3000/jatengs/" + form.id, {
              wisjateng: this.form.wisjateng,
              kotajateng: this.form.kotajateng,
              budayajateng: this.form.budayajateng,
              Transportasijateng: this.form.Transportasijateng,
              imagejateng: this.form.imagejateng,
            })
            .then((res) => {
              this.loadjateng();
              this.form.id = "";
              this.form.wisjateng = "";
              this.form.kotajateng = "";
              this.form.budayajateng = "";
              this.form.Transportasijateng = "";
              this.form.imagejateng = "";
              this.updateSubmit = false;
            })
            .catch((err) => {
              console.log(err);
            });
        });
    },
    del1(jabar) {
      axios.delete("http://localhost:3000/jabars/" + jabar.id).then((res) => {
        this.loadjabar();
        let index = this.jabars.indexOf(
          form.wisjabar,
          form.kota,
          form.budayajabar,
          form.Transportasijabar,
          form.imagejabar
        );
      });
    },
    del(jateng) {
      axios.delete("http://localhost:3000/jatengs/" + jateng.id).then((res) => {
        this.loadjateng();
        let index = this.jatengs.indexOf(
          form.wisjateng,
          form.kotajateng,
          form.budayajateng,
          form.Transportasijateng,
          form.imagejateng
        );
        this.jatengs.splice(index, 1);
      });
    },
    close() {
      window.location.reload();
    },
  },
};
</script>

<style>
</style>