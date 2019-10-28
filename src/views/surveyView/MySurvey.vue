<template>
  <v-container grid-list-md class="pt-5 mt-5">
    <div v-if="!this.$store.state.loading">
      <v-flex xs12 sm12 md12 xl12 class="center_card">
        <v-btn 
              large color="info"
              class="subheading v-btn--block
              font-weight-bold mt-4" round
              style="margin:0 auto; width:500px; height:50px;"
              @click="albaCreateFormRoute"
              >
              등록하기
            </v-btn>
        <div v-for="(alba, index) in albalist" :key="index">
          <v-card
            style="margin-top:50px;padding:20px; border-radius: 30px;"
            img="/static/alba_main.jpg"
          >
            <v-card-title>
              <v-chip class="body-2 ml-3 pa-2" color="info" dark>구인중</v-chip>
              <v-layout>
                <v-flex xs8 class="mt-3" style="margin-left:150px">
                  <span v-if="alba.TEXT.length > 10" class="headline white--text font-weight-bold">{{alba.TEXT.substr(0, 15) + "..."}}</span>
                  <span v-else class="headline white--text font-weight-bold">{{alba.TEXT}}</span>
                  <div class="white--text pt-1">작성날짜 : {{ alba.STARTDATE.substr(0,10) }}</div>
                </v-flex>
                <v-flex xs3>
                  <v-layout row wrap justify-start>
                    <div class="pb-2">
                      <v-icon large style="line-height:20px;">person</v-icon>
                      <span class="white--text ml-3">1人</span>
                    </div>
                    <div class="pb-2 mt-4">
                      <v-icon large style="line-height:20px;">event</v-icon>
                      <span class="white--text ml-3">~ {{ alba.STARTDATE.substr(0,10) }}</span>
                    </div>
                  </v-layout>
                </v-flex>
                <v-flex xs4>
                  <v-tooltip bottom>
                    <v-icon @click="surveyEdit" class="mr-5" slot="activator" size="65">edit</v-icon>
                    <span>구인공고 수정</span>
                  </v-tooltip>

                  <v-tooltip bottom>
                    <v-icon slot="activator" size="65" @click="surveyRemove">delete</v-icon>
                    <span>구인공고 삭제</span>
                  </v-tooltip>
                </v-flex>
              </v-layout>
            </v-card-title>
          </v-card>
        </div>
      </v-flex>
      <AddSurvey />
    </div>
    <Spinner v-else />
  </v-container>
</template>

<script>
import AddSurvey from "@/components/survey/AddSurvey";
import { mapState, mapMutations, mapActions } from "vuex";
import Spinner from "@/components/Spinner";
import swal from "sweetalert";
import { mySurvey } from "@/api/index";

export default {
  props: ["form_id"],
  name: "mysurvey",
  data() {
    return {
      page: 1,
      sale_check: 2,
      complete_check: 2,
      albalist: []
    };
  },
  components: { AddSurvey, Spinner },
  computed: {
    ...mapState(["mySurveyForm", "userinfo"]),
    SortmySurveyForm() {
      this.mySurveyForm.sort((x, y) => {
        return y.id - x.id;
      });
      return this.mySurveyForm;
    },
    
  },
  mounted() {
    this.FETCH_MY_SURVEY_FORM({
      id: this.userinfo.id
    });
    this.getMyAlbaList();
    console.log(this.albalist);
  },
  methods: {
    ...mapMutations(["SET_IS_ADD_SURVEY"]),
    ...mapActions([
      "FETCH_MY_SURVEY_FORM_TEST",
      "FETCH_MY_SURVEY_FORM",
      "REMOVE_MY_SURVEY"
    ]),
    getMyAlbaList() {
      fetch("http://15.164.224.74:3000/employerjoboffer?ID=1", {
        method: "GET"
      })
        .then(response => response.json())
        .then(responseJson => {
          this.albalist = responseJson.jobOffer;
        })
        .catch(error => {
          console.log("에러");
        });
    },
    noRedirectAnalysis() {
      swal("確認できません", "誰も応じなかったです。", "error", {
        button: "OK"
      });
    },
    surveyEdit() {
      swal({
        text: "정보를 수정하시겠어요?",
        icon: "warning",
        buttons: true,
        dangerMode: true
      });
    },
    surveyRemove() {
      swal({
        text: "모집을 취소하시겠습니까?",
        icon: "warning",
        buttons: true,
        dangerMode: true
      });
    },
    albaCreateFormRoute() {
        this.$router.push({name: 'albaCreateForm'})
    }
  }
};
</script>

<style scoped>
.center_card {
  margin: 0 auto;
}
* {
  text-decoration: none;
}
</style>