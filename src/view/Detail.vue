<template>
  <div>
    <div id="detail">
      <Navbar />
    </div>
    <!-- Button trigger modal -->
    <button
      style="margin-left: 74rem; margin-top: 5rem"
      type="button"
      class="btn btn-primary"
      data-bs-toggle="modal"
      data-bs-target="#exampleModal"
    >
      <i class="fas fa-plus"></i>ADD
    </button>

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
          <div class="modal-body">
            <form @submit.prevent="addjabar">
              <table>
                <tr>
                  <label for="">Pariwisata</label>
                  <br />
                  <!-- <td><input type="hidden" v-model="form.id" required></td> -->
                  <input type="text" v-model="formjabar.wisjabar" required />
                </tr>
                <tr>
                  <label for="">Kota</label>
                  <br />
                  <input type="text" v-model="formjabar.kota" required />
                </tr>
                <tr>
                  <label for="">Tradisi</label>
                  <br />
                  <input type="text" v-model="formjabar.budayajabar" required />
                </tr>
                <tr>
                  <label for="">Luas</label>
                  <br />
                  <input
                    type="text"
                    v-model="formjabar.Transportasijabar"
                    required
                  />
                </tr>
                <tr>
                  <label for="">Monumen</label>
                  <br />
                  <input type="text" v-model="formjabar.imagejabar" />
                </tr>
                <br />
                <button
                  type="button"
                  class="btn btn-secondary"
                  data-bs-dismiss="modal"
                  @click="close"
                >
                  Close
                </button>
                <button
                  class="btn btn-primary"
                  type="submit"
                  v-show="!updateSubmitJabar"
                >
                  <i class="fas fa-location-arrow"></i>Save Changes
                </button>
                <!-- jika tidak update maka tombol update tidak muncul -->
                <button
                  class="btn btn-success"
                  type="button"
                  v-show="updateSubmitJabar"
                  @click="update(formjabar)"
                >
                  <i class="fas fa-pen-fancy"></i>
                  Update
                </button>
              </table>
            </form>
          </div>
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
          <th scope="col">Action</th>
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
          <td style="text-align: center">
            <button class="Edit" @click="edit1(jabar)">
              <i class="fas fa-edit"></i>Edit
            </button>
            ||
            <button class="Delete" @click="del1(jabar)">
              <i class="fas fa-trash"></i>Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
    <!-- Table Jateng -->
    <!-- Button trigger modal -->
    <button
      style="margin-left: 74rem; margin-top: 5rem"
      type="button"
      class="btn btn-primary"
      data-bs-toggle="modal"
      data-bs-target="#jateng"
    >
      <i class="fas fa-plus"></i>ADD
    </button>
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
              Form<span v-show="!updateSubmitJateng"> Tambah</span
              ><span v-show="updateSubmitJateng"> Update</span>
            </h1>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
              @click="close"
            ></button>
          </div>
          <div class="modal-body">
            <form @submit.prevent="addjateng">
              <table>
                <tr>
                  <label for="">Pariwisata</label>
                  <br />
                  <td><input type="hidden" v-model="form.id" required /></td>
                  <input type="text" v-model="form.wisjateng" required />
                </tr>
                <tr>
                  <label for="">Kota</label>
                  <br />
                  <input type="text" v-model="form.kotajateng" required />
                </tr>
                <tr>
                  <label for="">Tradisi</label>
                  <br />
                  <input type="text" v-model="form.budayajateng" required />
                </tr>
                <tr>
                  <label for="">Luas</label>
                  <br />
                  <input
                    type="text"
                    v-model="form.Transportasijateng"
                    required
                  />
                </tr>
                <tr>
                  <label for="">Monumen</label>
                  <br />
                  <input type="text" v-model="form.imagejateng" />
                </tr>
                <br />
                <button
                  type="button"
                  class="btn btn-secondary"
                  data-bs-dismiss="modal"
                  @click="close"
                >
                  Close
                </button>
                <button
                  class="btn btn-primary"
                  type="submit"
                  v-show="!updateSubmitJateng"
                >
                  <i class="fas fa-location-arrow"></i>Save Changes
                </button>
                <!-- jika tidak update maka tombol update tidak muncul -->
                <button
                  class="btn btn-success"
                  type="button"
                  v-show="updateSubmitJateng"
                  @click="update2(form)"
                >
                  <i class="fas fa-pen-fancy"></i>
                  Update
                </button>
              </table>
            </form>
          </div>
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
          <th scope="col">Action</th>
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
          <td style="text-align: center">
            <button class="Edit" @click="edit(jateng)">
              <i class="fas fa-edit"></i>Edit
            </button>
            ||
            <button class="Delete" @click="del(jateng)">
              <i class="fas fa-trash"></i>Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
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
      formjabar: {
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
        this.form.wisjateng = "";
        this.form.kotajateng = "";
        this.form.budayajateng = "";
        this.form.Transportasijateng = "";
        this.form.imagejateng = "";
      });
    },
    edit1(jabar) {
      this.updateSubmitJabar = true;
      this.formjabar.id = jabar.id;
      this.formjabar.wisjabar = jabar.wisjabar;
      this.formjabar.kota = jabar.kota;
      this.formjabar.budayajabar = jabar.budayajabar;
      this.formjabar.Transportasijabar = jabar.Transportasijabar;
      this.formjabar.imagejabar = jabar.imagejabar;
    },
    edit(jateng) {
      this.updateSubmitJateng = true;
      this.form.id = jateng.id;
      this.form.wisjateng = jateng.wisjateng;
      this.form.kotajateng = jateng.kotajateng;
      this.form.budayajateng = jateng.budayajateng;
      this.form.Transportasijateng = jateng.Transportasijateng;
      this.form.imagejateng = jateng.imagejateng;
    },
    update(jabar) {
      return axios
        .put("http://localhost:3000/jabars/" + jabar.id, {
          wisjabar: this.formjabar.wisjabar,
          kota: this.formjabar.kota,
          budayajabar: this.formjabar.budayajabar,
          Transportasijabar: this.formjabar.Transportasijabar,
          imagejabar: this.formjabar.imagejabar,
        })
        .then((res) => {
          this.loadjabar();
          this.formjabar.id = "";
          this.formjabar.wisjabar = "";
          this.formjabar.kota = "";
          this.formjabar.budayajabar = "";
          this.formjabar.Transportasijabar = "";
          this.formjabar.imagejabar = "";
          this.updateSubmitJabar = false;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    update2(form) {
      return axios
        .put("http://localhost:3000/jatengs/" + form.id, {
          wisjateng: this.form.wisjateng,
          kotajateng: this.form.kotajateng,
          budayajateng: this.form.budayajateng,
          Transportasijateng: this.form.Transportasijateng,
          imagejateng: this.form.imagejateng,
        })
        .then((res) => {
          this.load();
          this.form.id = "";
          this.form.wisjateng = "";
          this.form.kotajateng = "";
          this.form.budayajateng = "";
          this.form.Transportasijateng = "";
          this.form.imagejateng = "";
          this.updateSubmitJateng = false;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    del1(jabar) {
      axios.delete("http://localhost:3000/jabars/" + jabar.id).then((res) => {
        this.loadjabar();
        let index = this.jabars.indexOf(
          formjabar.wisjabar,
          formjabar.kota,
          formjabar.budayajabar,
          formjabar.Transportasijabar,
          formjabar.imagejabar
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