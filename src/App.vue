<template>
  <v-app>
    <v-app-bar app color="deep-purple">
      <v-toolbar-title class="white--text"
        >Eagle Finance Services</v-toolbar-title
      >
      <v-spacer></v-spacer>
      <div class="hidden-xs-only">
        <v-btn
          v-for="item in menu"
          :key="item.title"
          :to="item.url"
          flat
          text
          rounded
          dark
          >{{ item.title }}</v-btn
        >
        <v-btn flat dark text rounded v-if="!authenticated" @click="login"
          >Log in
        </v-btn>
        <v-btn flat dark text rounded v-if="authenticated" @click="logout"
          >Log Out
        </v-btn>
      </div>
      <div class="hidden-sm-and-up">
        <v-app-bar-nav-icon
          @click="drawer = true"
          class="white--text"
        ></v-app-bar-nav-icon>
      </div>
    </v-app-bar>
    <v-navigation-drawer
      v-model="drawer"
      absolute
      temporary
      class="deep-purple"
    >
      <v-list>
        <v-list-item
          v-for="item in menu"
          :key="item.title"
          :to="item.url"
          class="white--text"
          >{{ item.title }}</v-list-item
        >
      </v-list>
      <div class="pa-2">
        <v-btn block v-if="!authenticated" @click="login">Login</v-btn>
        <v-btn block v-if="authenticated" @click="logout">Logout</v-btn>
      </div>
    </v-navigation-drawer>
    <v-content>
      <router-view />
    </v-content>
  </v-app>
</template>

<script>
import router from "./router";
import { APIService } from "./http/APIService";
const apiService = new APIService();

export default {
  name: "App",
  data: () => ({
    authenticated: false,
    dialog: false,
    drawer: false,
    menu: [
      { title: "Home", url: "/" },
      { title: "Customers", url: "/customer-list" },
      { title: "Stocks", url: "/stock-list" },
      { title: "Investments", url: "/investment-list" }
    ]
  }),

  mounted() {
    apiService
      .getCustomerList()
      .then(response => {
        this.authenticated = true;
      })
      .catch(error => {
        if (error.response.status === 401) {
          localStorage.removeItem("isAuthenticates");
          localStorage.removeItem("log_user");
          localStorage.removeItem("token");
          this.authenticated = false;
        }
      });
    console.log("this.authenticated--" + this.authenticated);
  },

  methods: {
    logout() {
      localStorage.removeItem("isAuthenticates");
      localStorage.removeItem("log_user");
      localStorage.removeItem("token");
      this.authenticated = false;
      // router.push('/');
      window.location = "/";
    },
    login() {
      router.push("/auth");
    }
  }
};
</script>
<style scoped>
main {
  background-image: url("assets/images/pb3.jpg");
  background-size: cover;
}
</style>
