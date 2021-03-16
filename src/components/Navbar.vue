<template>
  <nav>
    <div class="nav-wrapper green">
      <div class="container">
        <router-link to="/"> Home </router-link>
        <ul class="right">
          <li v-if="isLoggedIn"><router-link to="/">Dashboard</router-link></li>
          <li v-if="!isLoggedIn">
            <router-link to="/login">login</router-link>
          </li>
          <li v-if="isLoggedIn">
            <button v-on:click="logout" class="btn black">Logout</button>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>


<style>
.router-link-exact-active {
  color: black;
  font-weight: 800;
}
</style>

<script>
import firebase from "firebase";

export default {
  name: "navbar",
  data() {
    return {
      isLoggedIn: false,
      currentUser: false,
    };
  },
  created() {
    if (firebase.auth().currentUser) {
      this.isLoggedIn = true;
      this.currentUser = firebase.auth().currentUser.email;
    }
  },
  methods: {
    logout: function () {
      firebase
        .auth()
        .signOut()
        .then(() => {
          //   this.$router.push("/login"); not renderng navbar
          this.$router.go({ path: this.$router.path });
        });
    },
  },
};
</script>

