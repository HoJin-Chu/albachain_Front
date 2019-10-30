<template>
  <span>
    <div v-if="loading">
      <v-layout row wrap justify-space-around>
        <v-btn
          color="#29B6F6"
          dark
          fixed
          left
          bottom
          style="margin-bottom:270px;
        height:200px; margin-left:-30px;"
          @click.stop="drawer = !drawer"
        >
          <v-icon>arrow_forward_ios</v-icon>
        </v-btn>
        <v-flex xs9>
          <div class="display-1 font-weight-bold mb-5">
            <span
              class="info--text"
            >일했던 알바목록</span>
          </div>
          <v-data-table
            :headers="headers"
            :items="albaList"
            :search="search"
            :pagination.sync="pagination"
            class="elevation-1"
          >
            <template v-slot:items="props">
              <router-link
                :to=" {
                name : 'donationdetail',
                params: { donation_id: props.item.form_id }
              } "
              >
                <td
                  class="pa-5 text-xs-center font-weight-bold headline black--text"
                >{{ props.item[0] }}</td>
              </router-link>
              <td class="title">
                <span
                  style="color:#42A5F5"
                >{{new Date(parseInt(props.item[1])).getFullYear() }}년 {{new Date(parseInt(props.item[1])).getMonth()+1 }}월 {{new Date(parseInt(props.item[1])).getDay() }}일</span>
              </td>
              <td class="text-xs-center grey--text">8750원</td>
            </template>
          </v-data-table>
        </v-flex>
      </v-layout>
      <div class="text-xs-center pt-5">
        <v-pagination v-model="pagination.page" :length="pages"></v-pagination>
      </div>
    </div>
    <Spinner v-else />
  </span>
</template>

<script>
import myNav from "./myNav";
import { mapState } from "vuex";
import { mypage } from "@/api/index";
import Spinner from "@/components/Spinner";

export default {
  components: { myNav, Spinner },
  data() {
    return {
      drawer: null,
      loading: false,
      search: "",
      pagination: {},
      headers: [
        {
          text: "업체명",
          align: "center"
        },
        {
          text: "알바기간",
          align: "center"
        },
        {
          text: "급여",
          align: "center"
        }
      ],
      albaList: [],
      donationInfo: []
    };
  },
  mounted() {
    this.fetchDonatedonate();
    this.getMyAlbaList();
  },
  computed: {
    ...mapState(["userinfo"]),
    pages() {
      if (
        this.pagination.rowsPerPage == null ||
        this.pagination.totalItems == null
      )
        return 0;

      return Math.ceil(
        this.pagination.totalItems / this.pagination.rowsPerPage
      );
    },
    total() {
      var regexp = /\B(?=(\d{3})+(?!\d))/g;
      var totalCoin =
        this.donationInfo.reduce((acc, item) => acc + item.price, 0) + "";
      return totalCoin.replace(regexp, ",");
    }
  },
  methods: {
    getMyAlbaList() {
      fetch("http://15.164.224.74:3000/employeecareerlookup?ID=a", {
        method: "GET"
      })
        .then(response => response.json())
        .then(responseJson => {
          this.albaList = responseJson.recordArray;
          console.log(this.albaList);
        })
        .catch(error => {
          console.log(error);
        });
    },
    fetchDonatedonate() {
      this.loading = true;
      return mypage
        .FetchDonationDonate({ id: this.userinfo.id })
        .then(response => {
          console.log(response);
          this.donationInfo = response.list;
          this.loading = false;
        });
    },
    surveyPage() {
      this.$router.push({ name: "surveyhistory" });
    },
    marketPage() {
      this.$router.push({ name: "markethistory" });
    },
    foundationPage() {
      this.$router.push({ name: "foundationhistory" });
    },
    donatePage() {
      this.$router.push({ name: "donatehistory" });
    },
    walletPage() {
      this.$router.push({ name: "wallethistory" });
    }
  }
};
</script>

<style scoped>
.myhover_style {
  cursor: pointer;
  transition: background 0.7s ease;
}
.myhover_style:hover {
  background: #e0e0e0;
}
</style>