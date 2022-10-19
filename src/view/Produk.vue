<template>
  <div id="produk">
    <Navbar />
    <h1>Ini Halaman Produk Page</h1>
    <div class="tab">
      <div>
        <table class="table table-dark table-hover text-center">
          <thead>
            <tr>
              <th>Kota Administrasi</th>
              <th>Kecamatan</th>
              <th>Kelurahan</th>
              <th>Jumlah Penduduk</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="user in users" :key="user.id">
              <td>{{ user.kota }}</td>
              <td>{{ user.kecamatan }} Kecamatan</td>
              <td>{{ user.kelurahan }} Kelurahan</td>
              <td>{{ user.jumlah }}</td>
            </tr>
          </tbody>
        </table>
      </div>
      <div>
        <table class="table table-dark table-hover text-center">
          <thead>
            <tr>
              <th>Kota Administrasi</th>
              <th>Kecamatan</th>
              <th>Kelurahan</th>
              <th>Jumlah Penduduk</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="user in jatengs" :key="user.id">
              <td>{{ user.kota }}</td>
              <td>{{ user.kecamatan }} Kecamatan</td>
              <td>{{ user.kelurahan }} Kelurahan</td>
              <td>{{ user.jumlah }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
import axios from "axios";

export default {
  name: "ProdukPage",
  components: {
    Navbar,
  },
  data() {
    return {
      users: "",
      jatengs: "",
    };
  },
  mounted() {
    if (!sessionStorage.getItem("USER_DATA")) {
      this.$router.push("/");
    }
    this.loadUsers();
    this.loadJatengs();
  },
  methods: {
    loadUsers() {
      axios
        .get(" http://localhost:3000/users")
        .then((res) => {
          console.log(res.data);
          this.users = res.data; //respon dari rest api dimasukan ke users
        })
        .catch((err) => {
          console.log(err);
        });
    },
    loadJatengs() {
      axios
        .get(" http://localhost:3000/jatengs")
        .then((res) => {
          console.log(res.data);
          this.jatengs = res.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style scoped>
.tab {
  padding: 30px;
}
</style>