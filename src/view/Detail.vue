<template>
  <div id="detail">
    <Navbar />
    <h1>Ini Halaman Detail Page</h1>

    <div class="tab">
      <!-- bagian jakarta -->
      <div>
        <button
          type="button"
          class="btn btn-primary"
          data-bs-toggle="modal"
          data-bs-target="#exampleModal"
        >
          Add
        </button>
      </div>
      <br />
      <!-- tabel jakarta -->
      <div>
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
              <!-- <td>{{ index + 1 }}</td> -->
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

      <!-- bagian jateng -->
      <div>
        <button
          type="button"
          class="btn btn-primary"
          data-bs-toggle="modal"
          data-bs-target="#exampleModalJateng"
        >
          Add jateng
        </button>
      </div>
      <br />
      <!-- tabel jateng -->
      <div>
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
            <tr v-for="jateng in jatengs" :key="jateng.id">
              <td>{{ jateng.kota }}</td>
              <td>{{ jateng.kecamatan }} Kecamatan</td>
              <td>{{ jateng.kelurahan }} Kelurahan</td>
              <td>{{ jateng.jumlah }}</td>
              <td style="text-align: center">
                <button class="edit" @click="editJateng(jateng)">Edit</button>
                ||
                <button class="delete" @click="delJateng(jateng)">
                  Delete
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <!-- Modal jakarta -->
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
              from <span v-show="!updateSubmitJakarta">Tambah</span>
              <span v-show="updateSubmitJakarta">Update</span>
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
            <form @submit.prevent="add">
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label"
                  >Kota Administrasi</label
                >
                <input
                  type="text"
                  v-model="form.kota"
                  required
                  class="form-control"
                  id="exampleInputEmail1"
                  aria-describedby="emailHelp"
                />
              </div>
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label"
                  >Kecamatan</label
                >
                <input
                  type="text"
                  v-model="form.kecamatan"
                  required
                  class="form-control"
                  id="exampleInputEmail1"
                  aria-describedby="emailHelp"
                />
              </div>
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label"
                  >Kelurahan</label
                >
                <input
                  type="text"
                  v-model="form.kelurahan"
                  required
                  class="form-control"
                  id="exampleInputEmail1"
                  aria-describedby="emailHelp"
                />
              </div>
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label"
                  >Jumlah Penduduk</label
                >
                <input
                  type="text"
                  v-model="form.jumlah"
                  required
                  class="form-control"
                  id="exampleInputEmail1"
                  aria-describedby="emailHelp"
                />
              </div>
              <br />
              <button
                type="button"
                class="btn btn-secondary"
                data-bs-dismiss="modal"
              >
                Close
              </button>
              ||
              <button
                type="submit"
                class="btn btn-primary"
                data-bs-dismiss="modal"
              >
                Save changes
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>

    <!-- modal jateng -->
    <div
      class="modal fade"
      id="exampleModalJateng"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="exampleModalLabel">
              from <span v-show="!updateSubmitJateng">Tambah</span>
              <span v-show="updateSubmitJateng">Update</span>
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
            <form @submit.prevent="addJateng">
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label"
                  >Kota Administrasi</label
                >
                <input
                  type="text"
                  v-model="formJatengs.kota"
                  required
                  class="form-control"
                  id="exampleInputEmail1"
                  aria-describedby="emailHelp"
                />
              </div>
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label"
                  >Kecamatan</label
                >
                <input
                  type="text"
                  v-model="formJatengs.kecamatan"
                  required
                  class="form-control"
                  id="exampleInputEmail1"
                  aria-describedby="emailHelp"
                />
              </div>
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label"
                  >Kelurahan</label
                >
                <input
                  type="text"
                  v-model="formJatengs.kelurahan"
                  required
                  class="form-control"
                  id="exampleInputEmail1"
                  aria-describedby="emailHelp"
                />
              </div>
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label"
                  >Jumlah Penduduk</label
                >
                <input
                  type="text"
                  v-model="formJatengs.jumlah"
                  required
                  class="form-control"
                  id="exampleInputEmail1"
                  aria-describedby="emailHelp"
                />
              </div>
              <br />
              <button
                type="button"
                class="btn btn-secondary"
                data-bs-dismiss="modal"
              >
                Close
              </button>
              ||
              <button
                type="submit"
                class="btn btn-primary"
                data-bs-dismiss="modal"
                v-show="!updateSubmitJateng"
              >
                Add
              </button>
              <button
                type="submit"
                class="btn btn-primary"
                data-bs-dismiss="modal"
                v-show="updateSubmitJateng"
                @click="updateJateng(formJatengs)"
              >
                Save changes
              </button>
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
  name: "DetailPage",
  components: {
    Navbar,
  },
  mounted() {
    if (!sessionStorage.getItem("USER_DATA")) {
      this.$router.push("/");
    }
    this.loadUsers();
    this.loadJatengs();
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
      updateSubmitJakarta: false,
      formJatengs: {
        id: "",
        kota: "",
        kecamatan: "",
        kelurahan: "",
        jumlah: "",
      },
      jatengs: "",
      updateSubmitJateng: false,
    };
  },
  methods: {
    // methods users
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
    add() {
      axios.post("http://localhost:3000/users/", this.form).then(() => {
        this.loadUsers();
        this.form.kota = "";
        this.form.kecamatan = "";
        this.form.kelurahan = "";
        this.form.jumlah = "";
      });
    },
    edit(user) {
      this.updateSubmit = true;
      this.form.id = user.id;
      this.form.kota = user.kota;
      this.form.kecamatan = user.kecamatan;
      this.form.kelurahan = user.kelurahan;
      this.form.jumlah = user.jumlah;
    },
    update(form) {
      return axios
        .put("http://localhost:3000/users/" + form.id, {
          kota: this.form.kota,
          kecamatan: this.form.kecamatan,
          kelurahan: this.form.kelurahan,
          jumlah: this.form.jumlah,
        })
        .then(() => {
          this.form.id = "";
          this.form.kota = "";
          this.form.kecamatan = "";
          this.form.kelurahan = "";
          this.form.jumlah = "";
          this.updateSubmit = false;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    del(user) {
      axios.delete("http://localhost:3000/users/" + user.id).then(() => {
        let index = this.users.indexOf(
          this.kota,
          this.kecamatan,
          this.kelurahan,
          this.jumlah
        );
        this.users.splice(index, 1);
      });
    },

    // methods jatengs
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

    addJateng() {
      axios
        .post("http://localhost:3000/jatengs/", this.formJatengs)
        .then(() => {
          this.loadJatengs();
          this.formJatengs.kota = "";
          this.formJatengs.kecamatan = "";
          this.formJatengs.kelurahan = "";
          this.formJatengs.jumlah = "";
        });
    },
    editJateng(jateng) {
      this.updateSubmitJateng = true;
      this.formJatengs.id = jateng.id;
      this.formJatengs.kota = jateng.kota;
      this.formJatengs.kecamatan = jateng.kecamatan;
      this.formJatengs.kelurahan = jateng.kelurahan;
      this.formJatengs.jumlah = jateng.jumlah;
    },
    updateJateng(formJatengs) {
      return axios
        .put("http://localhost:3000/jatengs/" + formJatengs.id, {
          kota: this.formJatengs.kota,
          kecamatan: this.formJatengs.kecamatan,
          kelurahan: this.formJatengs.kelurahan,
          jumlah: this.formJatengs.jumlah,
        })
        .then(() => {
          this.loadJatengs();
          this.formJatengs.id = "";
          this.formJatengs.kota = "";
          this.formJatengs.kecamatan = "";
          this.formJatengs.kelurahan = "";
          this.formJatengs.jumlah = "";
          this.updateSubmit = false;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    delJateng(jateng) {
      axios.delete("http://localhost:3000/jatengs/" + jateng.id).then(() => {
        let index = this.jatengs.indexOf(
          this.kota,
          this.kecamatan,
          this.kelurahan,
          this.jumlah
        );
        this.jatengs.splice(index, 1);
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
.tab {
  padding: 30px;
}
</style>