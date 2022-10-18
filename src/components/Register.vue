<template>
    <div class="kotak_login">
        <h4 class="tulisan_login">Register</h4>
        <form @submit="register">
            <label class="reg">Username</label>
            <input 
             type="text"
             name="username"
             v-model="username"
             class="form_login"
             placeholder="Username" 
             required
             />
             <label class="reg">Password</label>
             <input 
             type="password"
             name= "password" 
             v-model="password"
             class="form_login"
             placeholder="Password" 
             required
             />
             <button type="submit" class="btn btn-success poll" @click="register">Register</button>
             <center>
                 <p class="f00ter">
                 <a href="/" class="registerdonk">Login</a>
                 <span class="notReg"> Jika Telah Memiki Akun</span>
                 </p>
             </center>
        </form>
    </div>
</template>

<script>
import axios from 'axios';

export default {
        name: "RegisterPage",
        data() {
            return {
                username: "",
                password: "",
            };
        },
        methods: {
            async register(e) {
                e.preventDefault();
                // memasukkan data input ke json
                const payload = {
                    username: this.username,
                    password: this.password,
                    role: "user"
                };
                const registrasi = await axios.post(
                    "http://localhost:3000/akuns",
                    payload
                );
                // fungsi setelah registrasi langsung page home
                var convertToString = JSON.stringify(registrasi.data);
                sessionStorage.setItem("USER_DATA", convertToString);
                this.$emit("toggleBar");
                this.$router.push("/");
            },
        },
        
};
</script>

<style>
h4 {
  text-align: center;
  /*ketebalan font*/
  font-weight: 300;
  color: white;
}
.tulisan_login {
  text-align: center;
  /*membuat semua huruf menjadi kapital*/
  text-transform: uppercase;
  color: white;
}
.reg {
  font-size: 11pt;
  color: white;
}
.kotak_login {
  border: 1px solid #232323;
  border-radius: 10%;
  width: 350px;
  background-color: gray;
  /*meletakkan form ke tengah*/
  margin: 80px auto;
  padding: 30px 20px;
  /* color: white; */
}
.form_login {
  /*membuat lebar form penuh*/
  box-sizing: border-box;
  width: 100%;
  padding: 10px;
  font-size: 11pt;
  margin-bottom: 20px;
  /* color: white; */
}
.link {
  color: lightgreen;
  text-decoration: none;
  font-size: 10pt;
}
.aa {
  border: 1px solid black;
  border-radius: 10px;
  background-color: aliceblue;
  margin-left: 50px;
  margin-right: 50px;
  padding: 5px;
  text-align: center;
}
.f00ter {
  text-align: end;
  margin-top: 20px;
  margin-bottom: -20px;
}
.f00ter a {
  text-decoration: none;
  color: white;
}
.registerdonk:hover {
  text-decoration: underline;
}
.registerdonk{
    color: lightgreen;
}
.poll {
  width: 100%;
}
.notReg {
  padding-left: 2px;
}
</style>