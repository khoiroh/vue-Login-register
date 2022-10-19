<template>
  <div id="home">
    <Navbar />
    <h1>Ini Halaman Home Page</h1>

    <div class="tab">
        <div>
      <h3>DKI JAKARTA</h3>
      <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
  Add
</button></div>
    <br>
      <table class="table table-dark table-hover text-center">
        <thead>
        <tr>
          <th>Kota Administrasi</th>
          <th>Kecamatan</th>
          <th>Kelurahan</th>
          <th>Jumlah Penduduk</th>
          <th>Action</th>
        </tr>
        </thead>
        <tbody>

        <tr v-for="user in users" :key="user.id">
          <td>{{ user.kota }}</td>
          <td>{{ user.kecamatan }} Kecamatan</td>
          <td>{{ user.kelurahan }} Kelurahan</td>
          <td>{{ user.jumlah }}</td>
          <td style="text-align: center">
            <button class="edit" @click="edit(user)">Edit</button> ||
            <button class="delete" @click="del(user)">Delete</button>
          </td>

        </tr>
        </tbody>

      </table>
    </div>
    <!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h1 class="modal-title fs-5" id="exampleModalLabel">
            from <span v-show="!updateSubmitJakarta">Tambah</span>
            <span v-show="updateSubmitJakarta">Update</span>
        </h1>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close" @click="close"></button>
      </div>
      <div class="modal-body">
    <form @submit.prevent="add">
        <div class="mb-3">
            <label for="exampleInputEmail1" class="form-label">Kota Administrasi</label>
            <input type="text" v-model="form.kota" required  class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
        </div>
        <div class="mb-3">
            <label for="exampleInputEmail1" class="form-label">Kecamatan</label>
            <input type="text" v-model="form.kecamatan" required  class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
        </div>
        <div class="mb-3">
            <label for="exampleInputEmail1" class="form-label">Kelurahan</label>
            <input type="text" v-model="form.kelurahan" required  class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
        </div>
        <div class="mb-3">
            <label for="exampleInputEmail1" class="form-label">Jumlah Penduduk</label>
            <input type="text" v-model="form.jumlah" required  class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
        </div>
        <br>
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal" >Close</button> || <button type="submit" class="btn btn-primary"  data-bs-dismiss="modal">Save changes</button>
    </form>
      </div>
      </div>
  </div>
</div>
  </div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
import axios from "axios";

export default {
  name: "HomePage",
  components: {
    Navbar,
  },
  mounted() {
    this.load();
    if (!sessionStorage.getItem("USER_DATA")) {
      this.$router.push("/");
    }
  },
  data() {
    return {
      form: {
        id: "",
        kota: "",
        kecamatan: "",
        kelurahan: "",
        jumlah: "",
      },
      users: "",
      updateSubmit: false,
    };
  },
  methods: {
    load() {
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
    add() {
      axios.post("http://localhost:3000/users/", this.form).then(() => {
        this.load();
        this.form.kota = "";
        this.form.kecamatan = "";
        this.form.kelurahan = "";
        this.form.jumlah = "";
      });
    },
      edit(user){
        this.updateSubmit = true
        this.form.id = user.id
        this.form.kota = user.kota
        this.form.kecamatan = user.kecamatan
        this.form.kelurahan = user.kelurahan
        this.form.jumlah = user.jumlah
      },
       update(form){
             return axios.put('http://localhost:3000/users/' + form.id ,
             {
             kota: this.form.kota,
             kecamatan : this.form.kecamatan,
              kelurahan: this.form.kelurahan,
              jumlah: this.form.jumlah,
              },
              ).then(() => {
             this.load()
             this.form.id = ''
             this.form.kota = ''
            this.form.kecamatan = ''
            this.form.kelurahan = ''
            this.form.jumlah = ''
            this.updateSubmit = false
          }).catch((err) => {
            console.log(err);

          });
        },
        del(user){
          axios.delete('http://localhost:3000/users/' + user.id).then(() =>{
              this.load()
              let index = this.users.indexOf(
              this.kota,
              this.kecamatan,
              this.kelurahan,
              this.jumlah,
              );
              this.users.splice(index,1);
          });
       },
    //    close
    close() {
        window.location.reload();
    },
  },
};
</script>

<style scoped>
.tab{
    padding: 30px;
}
</style>