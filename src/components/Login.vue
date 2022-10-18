<template>
    <div class="kotak_login">
        <h4 class="tulisan_login">Silahkan Login</h4>
        <form @submit="login">
            <label >Username</label>
            <input 
            type="text"
            required
            name="username"
            v-model="form.username"
            class="form_login"
            placeholder="Masukan Username atau email.."
            />
            <label>Password</label>
            <input 
            type="password"
            name="password"
            v-model="form.password"
            class="form_login"
            placeholder="Masukan Password.."
            required
            />
            <button type="submit" class="btn btn-primary poll">Login</button>
        <br>
        <br>
        <center>
            <span>Belum Punya Akun</span><a href="/register">Silahkan Register</a>
        </center>
        </form>
    </div>
</template>

<script>
// import axios
import axios from "axios"

export default {
    name: 'LoginPage',
    data() {
        return {
            form: {
                username: "",
                password: "",
                useres: {},
            },
        };
    },
    methods: {
        // menjalankan 2 fungsi mengambil data pada json dan mencari data yg sama diinputkan
        async getUser() {
            const user = await axios.get(" http://localhost:3000/akuns");
            this.useres = user.data;
        },
        // fungsi tombol login
        login(e) {
            e.preventDefault();
            const login = this.useres.find(
                (data) =>
                data.username === this.form.username &&
                data.password === this.form.password
            );
            // kondisi jika akun benar akan langsung masuk ke page home kalo salah muncul alert
           if (login  === undefined) {
                alert("Username Or Password Not Found");
            } else{
                var convertToString = JSON.stringify(login);
                sessionStorage.setItem("USER_DATA", convertToString);
                sessionStorage.setItem("role",login.role)
                this.$router.push("/home");
                window.location.reload();
            }
        },
    },
    mounted() {
        this.getUser();
        // fungsi toggle pada app.vue
         this.$emit("toggleBar");
    },
};
</script>