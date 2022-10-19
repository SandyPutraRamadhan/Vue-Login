<template>
  <div>
    <div id="home">
        <Navbar />
         </div>
        <!-- Button trigger modal -->
<button style="margin-left: 74rem; margin-top: 5rem;" type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
 <i class="fas fa-plus"></i>ADD
</button>

 <!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h1 class="modal-title fs-5" id="exampleModalLabel">Form<span v-show="!updateSubmit"> Tambah</span><span v-show="updateSubmit"> Update</span></h1>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close" @click="close"></button>
      </div>
      <div class="modal-body">
       <form @submit.prevent="add">
        <table>
          <tr>
           <label for="">Pariwisata</label>
           <br>
            <!-- <td><input type="hidden" v-model="form.id" required></td> -->
            <input type="text" v-model="form.wis" required />
          </tr>
          <tr>
            <label for="">Kota/Daerah Ibu Kota Jakarta</label>
            <br>
            <input type="text" v-model="form.kotajakar" required />
          </tr>
          <tr>
            <label for="">Tradisi</label>
            <br>
            <input type="text" v-model="form.budayajakar" required />
          </tr>
          <tr>
            <label for="">Luas</label>
            <br>
            <input type="text" v-model="form.Luasjakar" required />
          </tr>
          <tr>
            <label for="">Monumen</label>
            <br>
            <input type="text" v-model="form.image">
          </tr>
          <br />
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal" @click="close">Close</button>
        <button class="btn btn-primary" type="submit" v-show="!updateSubmit">
            <i class="fas fa-location-arrow"></i>Save Changes
          </button>
          <!-- jika tidak update maka tombol update tidak muncul -->
           <button
            class="btn btn-success"
            type="button"
            v-show="updateSubmit"
            @click="update(form)"
          ><i class="fas fa-pen-fancy"></i>
            Update
          </button>
          </table>
      </form>
      </div>
    </div>
  </div>
</div>   
    <!-- Table Data -->
    <div class="tabAll">
    <table class="table table-primary table-hover">
      <thead>
    <tr>
      <th scope="col">No.</th>
      <th scope="col">Wisata</th>
      <th scope="col">Kota/Daerah</th>
      <th scope="col">Tradisi</th>
      <th scope="col">Luas</th>
      <th scope="col">Monumen</th>
      <th scope="col">Action</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(jakar, index) in jakartas" :key="jakar.id">
        <td>{{ index + 1 }}</td>
      <td>{{ jakar.wis }}</td>
      <td>{{ jakar.kotajakar }}</td>
      <td>{{ jakar.budayajakar }}</td>
      <td>{{ jakar.Luasjakar }}</td>
      <td><img :src="jakar.image" alt="" width="100" height="100" /></td>
      <td style="text-align: center">
        <button data-bs-toggle="modal" data-bs-target="#exampleModal" class="Edit" @click="edit(jakar)"><i class="fas fa-edit"></i>Edit</button> ||
          <button class="Delete" @click="del(jakar)"><i class="fas fa-trash"></i>Delete</button>
      </td>
    </tr>
  </tbody>
    </table>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import Navbar from "../components/Navbar.vue";
import axios from "axios";
export default {
  name: "HomeE",
  components:{
        Navbar
    },
    mounted() {
        if (!sessionStorage.getItem("USER_DATA")) {
            this.$router.push("/");
        }
    },
  data() {
    return {
      form: {
        id: "",
        wis: "",
        kotajakar: "",
        budayajakar: "",
        Luasjakar: "",
        image: "",
      },
      jakartas: "",
      updateSubmit: false,
    };
  },
  mounted() {
    this.load();
  },
  methods: {
    load() {
      axios
        .get("http://localhost:3000/jakartas")
        .then((res) => {
          this.jakartas = res.data; 
        })
        .catch((err) => {
          console.log(err);
        });
    },
    add() {
      axios.post("http://localhost:3000/jakartas/", this.form).then((res) => {
        this.load();
        this.form.id = "";
        this.form.wis = "";
        this.form.kotajakar = "";
        this.form.budayajakar = "";
        this.form.Luasjakar = "";
        this.form.image = "";
      });
      window.location.reload();
    },
    edit(jakar) {
      this.updateSubmit = true;
      this.form.id = jakar.id;
      this.form.wis = jakar.wis;
      this.form.kotajakar = jakar.kotajakar;
      this.form.budayajakar = jakar.budayajakar;
      this.form.Luasjakar = jakar.Luasjakar;
      this.form.image = jakar.image;
    },
    update(form) {
      return axios
        .put("http://localhost:3000/jakartas/" + form.id, {
          wis: this.form.wis,
          kotajakar: this.form.kotajakar,
          budayajakar: this.form.budayajakar,
          Luasjakar: this.form.Luasjakar,
          image: this.form.image,
        })
        .then((res) => {
          this.load();
          this.form.id = "";
          this.form.wis = "";
          this.form.kotajakar = "";
          this.form.budayajakar = "";
          this.form.Luasjakar = "";
          this.form.image = "";
          this.updateSubmit = false;
          window.location.reload();
        })
        .catch((err) => {
          console.log(err);
        });
    },
    del(user) {
      axios.delete("http://localhost:3000/jakartas/" + user.id).then((res) => {
        this.load();
        let index = this.jakartas.indexOf(
          form.wis,
          form.kotajakar,
          form.budayajakar,
          form.Luasjakar,
          form.image
        );
        this.jakartas.splice(index, 1);
      });
    },
    // Close
    close() {
        window.location.reload();
    },
  },
};
</script>

<style>
.tabAll {
    margin :0 110px;
}
</style>