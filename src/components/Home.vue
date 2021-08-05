<template>
  <v-main>
    <v-container fluid>
      <v-row>
        <v-col align="center" justify="center" cols="12">
          <blockquote class="white--text">
            <h2>&#8220;Welcome {{ validUserName }}!&#8221;</h2>
            <footer>
              <medium>
                <em
                  >&mdash;Eagle Financial Services, your Midwest Financial
                  Services Partner&mdash;</em
                >
              </medium>
            </footer>
          </blockquote>
        </v-col>
      </v-row>
    </v-container>

    <v-container fluid>
      <v-row align="center" justify="center">
        <v-col cols="12" sm="10" md="10">
          <v-card class="elevation-2">
            <v-container fluid grid-list-md>
              <v-row>
                <v-col>
                  <v-card>
                    <v-img
                      :src="require('@/assets/images/c1.png')"
                      height="200px"
                    >
                    </v-img>
                    <v-card-text>
                      <div class="blue--text text-h6">
                        Customers
                      </div>
                    </v-card-text>
                    <v-card-actions>
                      <v-btn
                        flat
                        color="#B388FF"
                        class="white--text"
                        @click="viewCustomers"
                        >View Details</v-btn
                      >
                    </v-card-actions>
                  </v-card>
                </v-col>
                <v-col>
                  <v-card>
                    <v-img
                      :src="require('@/assets/images/i1.png')"
                      height="200px"
                    >
                    </v-img>
                    <v-card-text>
                      <div class="blue--text text-h6">
                        Investments
                      </div>
                    </v-card-text>
                    <v-card-actions>
                      <v-btn
                        flat
                        color="#B388FF"
                        class="white--text"
                        @click="viewInvestments"
                        >View Details</v-btn
                      >
                    </v-card-actions>
                  </v-card>
                </v-col>
                <v-col>
                  <v-card>
                    <v-img
                      :src="require('@/assets/images/s1.png')"
                      height="200px"
                    >
                    </v-img>
                    <v-card-text>
                      <div class="blue--text text-h6">
                        Stocks
                      </div>
                    </v-card-text>
                    <v-card-actions>
                      <v-btn
                        flat
                        color="#B388FF"
                        class="white--text"
                        @click="viewStocks"
                        >View Details</v-btn
                      >
                    </v-card-actions>
                  </v-card>
                </v-col>
              </v-row>
            </v-container>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
</template>

<script>
import router from "../router";

export default {
  name: "Home",
  data: () => ({
    validUserName: "Guest"
  }),
  mounted() {
    this.getUser();
  },
  methods: {
    viewCustomers() {
      router.push("/customer-list");
    },
    viewInvestments() {
      router.push("/investment-list");
    },
    viewStocks() {
      router.push("/stock-list");
    },
    getUser() {
      if (
        localStorage.getItem("isAuthenticates") &&
        JSON.parse(localStorage.getItem("isAuthenticates")) === true
      ) {
        this.validUserName = JSON.parse(localStorage.getItem("log_user"));
      }
    }
  }
};
</script>
