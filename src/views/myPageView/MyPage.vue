/* 마이페이지 */

<template>
  <v-container grid-list-md text-xs-center class="pa-5 mt-5" style="max-width: 100vw; padding:0px;">
    <div v-if="this.$route.name == 'mypage'">
      <v-img style="margin-bottom:-50px; margin-right:-50px;">
        <div class="display-2 pa-5 mt-5 font-weight-bold">
          <span class="blue--text">마이페이지</span>
        </div>
        <v-layout row wrap align-center justify-center class="pt-2 ml-5">
          <v-flex d-flex xs12 sm3 class="mr-5">
            <v-card class="border_round elevation-4">
              <v-card-title style="background-color:#66B3FF">
                <div style="margin:0 auto">
                  <div class="display-1 font-weight-bold py-1 white--text">고용주</div>
                </div>
              </v-card-title>
              <v-card flat :to="{name: 'surveyhistory'}">
                <div class="hover_style" style="margin:0 auto">
                  <div class="title font-weight-bold py-4">내가 작성한 공고목록</div>
                </div>
              </v-card>
              <v-card flat :to="{name: 'markethistory'}">
                <div class="hover_style" style="margin:0 auto">
                  <div class="title font-weight-bold py-4">승인 대기중인 공고목록</div>
                </div>
              </v-card>
            </v-card>
          </v-flex>
          <v-flex d-flex xs12 sm3 class="mr-5">
            <v-card class="border_round elevation-4">
              <v-card-title style="background-color:#66B3FF">
                <div style="margin:0 auto">
                  <div class="display-1 font-weight-bold py-1 white--text">아르바이트생</div>
                </div>
              </v-card-title>
              <v-card v-if="userinfo.is_donator ==1" flat :to="{name: 'foundationhistory'}">
                <div class="hover_style" style="margin:0 auto">
                  <div class="title font-weight-bold py-4">내가 알했던 공고목록</div>
                </div>
              </v-card>
              <v-card flat :to="{name: 'employeehistory'}">
                <div class="hover_style py-4" style="margin:0 auto">
                  <div class="title font-weight-bold" :style="styleObject">내가 일했던 알바목록</div>
                </div>
              </v-card>
            </v-card>
          </v-flex>
          <v-flex d-flex xs12 sm3 class="mr-5">
            <v-card class="border_round elevation-4">
              <v-card-title style="background-color:#66B3FF">
                <div style="margin:0 auto">
                  <div class="display-1 font-weight-bold py-1 white--text">정보 수정</div>
                </div>
              </v-card-title>
              <v-card flat :to="{name: 'wallethistory'}">
                <div class="hover_style py-4" style="margin:0 auto">
                  <div class="title font-weight-bold py-4">내 정보 보기</div>
                </div>
              </v-card>
            </v-card>
          </v-flex>
        </v-layout>
      </v-img>
    </div>
    <div v-else>
      <router-view />
    </div>
  </v-container>
</template>

<script>
import { mapState } from "vuex";
import { userInformation } from "@/api/index";

export default {
  data() {
    return {
      styleObject: "",
      inocoin: {}
    };
  },
  computed: {
    ...mapState(["userinfo"]),
    totalCoin() {
      var regexp = /\B(?=(\d{3})+(?!\d))/g;
      var inoValue = this.inocoin.current_ino + "";
      return inoValue.replace(regexp, ",");
    }
  },
  created() {
    if (!this.userinfo.is_donator == 1) {
      return (this.styleObject = "margin-top:8% ; padding-bottom:8%");
    }
  },
  mounted() {
    this.fetchCoin();
  },
  methods: {
    fetchCoin() {
      return userInformation
        .userCoin({ id: this.userinfo.id })
        .then(response => {
          this.inocoin = response;
        });
    }
  }
};
</script>

<style scoped>
#btn_center {
  border-radius: 5%;
  margin: 0 auto;
  width: 80%;
}
.border_round {
  border-radius: 20px;
}
.hover_style {
  cursor: pointer;
  transition: background 0.3s ease;
  border-top: 1px solid lightgrey;
}
.border {
  border-top: 1px solid lightgrey;
}
.hover_style:hover {
  background: #eeeeee;
}
</style>