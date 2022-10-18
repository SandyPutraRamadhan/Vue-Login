<template>
  <nav class="navbar navbar-expand-lg bg-dark">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Navbar</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item" v-if="AdminAccess">
            <router-link class="nav-link" to="/home">Home</router-link>
          </li>
          <li class="nav-item" v-if="AdminAccess">
            <router-link class="nav-link" to="/about">About</router-link>
          </li>
          <li class="nav-item" v-if="AdminAccess">
            <router-link class="nav-link" to="/contact">Contact</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/product">Product</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/detail">Detail</router-link>
          </li>
          <li class="nav-item" @click="out">
            <router-link to="/" class="nav-link log"
              >Log Out</router-link
            >
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "NavComp",
  computed: {
    AdminAccess() {
      return sessionStorage.getItem("role") === "admin";
    }
  },
  methods: {
    out() {
      sessionStorage.clear();
      this.$router.push("/");
    },
  },
};
</script>

<style scoped>
a {
  color: white;
}
.log {
  margin-left: 850px;
}
</style>