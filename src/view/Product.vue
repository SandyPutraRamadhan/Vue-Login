<template>
    <div id="product">
        <Navbar />
        <h1>Ini Halaman Product Page</h1>
    </div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
export default {
    name: "ProductPage",
    components:{
        Navbar
    },
    mounted() {
        if (!sessionStorage.getItem("USER_DATA")) {
            this.$router.push("/");
        }
    },
}
</script>
