<template>
    <div class="kotak_login">
        <h4 class="tulisan_login">Register</h4> 
        <form @submit="register">
            <label>Username</label>
            <input 
            type="text"
            name="username"
            v-model="username"
             required
            class="form_login"
            placeholder="Username atau email .."
            />
            <br />
            <label>password</label>
            <input 
            type="text"
            name="password"
            v-model="password"
            required
            class="form_login"
            placeholder="Password.."
            />
            <button type="submit" class="btn btn-primary poll" >Register</button>
            <br />
            <br />
             <center>
            <span>Bila Sudah Punya Akun </span><a href="/">Silahkan Login</a>
        </center>
        <br />
        </form>
    </div>
</template>
<script>
import axios from "axios";

export default {
  name: 'RegisterPage',
  data() {
    return{
        username: "",
        password: "",
    };
  },
  mounted() {
    this.$emit("toggleBar");
  },
  methods: {
    async register(e) {
       e.preventDefault();
       const payload = {
        username: this.username,
        password: this.password,
        role: "siswa",
       };
         const registrasi = await axios.post(
                " http://localhost:3000/akuns",
                payload
            );
            var convertToString = JSON.stringify(registrasi.data);
            sessionStorage.setItem("USER_DATA", convertToString);
            this.$emit("toggleBar");
            this.$router.push("/")
        },
    },
};
</script>

<style>
h1 {
  text-align: center;
  /*ketebalan font*/
  font-weight: 300;
}
.tulisan_login {
  text-align: center;
  /*membuat semua huruf menjadi kapital*/
  text-transform: uppercase;
}
label {
  font-size: 11pt;
}
.kotak_login {
  border: 1px solid #232323;
  border-radius: 10%;
  width: 350px;
  background-color: white;
  /*meletakkan form ke tengah*/
  margin: 80px auto;
  padding: 30px 20px;
}
.form_login {
  /*membuat lebar form penuh*/
  box-sizing: border-box;
  width: 100%;
  padding: 10px;
  font-size: 11pt;
  margin-bottom: 20px;
}
.link {
  color: #232323;
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
}
.registerdonk:hover {
  text-decoration: underline;
}
.poll {
  width: 100%;
}
.notReg {
  padding-left: 2px;
}
</style>