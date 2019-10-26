<template>
  <v-container grid-list-md class="pt-5 mt-5">
      <div v-if="!this.$store.state.loading">
        <v-flex xs12 sm12 md12 xl11 class="center_card">
            <v-btn 
              large color="info"
              class="subheading v-btn--block
              font-weight-bold mt-4" round
              style="margin:0 auto; width:500px; height:50px;"
              @click="albaCreateFormRoute"
              >
              등록하기
            </v-btn>
          <div v-for="(form, index) in SortmySurveyForm" :key="index">
            <v-card 
              style="margin-top:50px;padding:20px;"
            >
              <v-card-title>
                <v-chip
                class="body-2 ml-3 pa-2" color="info" dark>回答中..</v-chip>
                <v-layout>
                  <v-flex xs7 class="mt-3" style="margin-left:150px">
                    <span class="headline font-weight-bold">asd</span>
                    <div class="grey--text pt-1">作成日時 : asd</div>
                  </v-flex>
                  <v-flex xs3>
                    <v-layout row wrap justify-start>
                      <div class="pb-2"><v-icon large style="line-height:20px;">person</v-icon><span class="ml-3">asda / asd 人</span></div>
                      <div class="pb-2 mt-4"><v-icon large style="line-height:20px;">event</v-icon><span class="ml-3">asd ~ asd</span></div>
                    </v-layout>
                  </v-flex>
                  <v-flex xs4>
                    <v-tooltip bottom>
                      <v-icon
                        class="mr-5"
                        @click="surveySales(index,form.id)" 
                        slot="activator" 
                        size="65"
                      >
                        shopping_cart
                      </v-icon>
                      <span>アンケートの販売</span>
                    </v-tooltip>
                    
                    <v-tooltip bottom>
                      <v-icon 
                        slot="activator" size="65" @click="surveyRemove"
                      >delete
                      </v-icon>
                      <span>削除</span>
                    </v-tooltip>
                  </v-flex>
                </v-layout>
              </v-card-title>
            </v-card>
          </div>
          
        </v-flex>
        <AddSurvey/>
      </div>
      <Spinner v-else/>
  </v-container>
</template>

<script>
  import AddSurvey                              from '@/components/survey/AddSurvey'
  import { mapState, mapMutations, mapActions } from 'vuex'
  import Spinner                                from '@/components/Spinner'
  import swal                                   from 'sweetalert'
  import { mySurvey }                           from '@/api/index'
  
  export default {
    props: ['form_id'],
    name: 'mysurvey',
    data() {
      return {
        page : 1,
        sale_check: 2,
        complete_check: 2

      }
    },
    components: { AddSurvey, Spinner },
    computed: {
      ...mapState([ 'mySurveyForm', 'userinfo' ]),
      SortmySurveyForm() {
        this.mySurveyForm.sort((x, y) => { return y.id- x.id })
        return this.mySurveyForm
      },
    },
    mounted() {
      this.FETCH_MY_SURVEY_FORM({
        id: this.userinfo.id
      })
    },
    methods: {
      ...mapMutations(['SET_IS_ADD_SURVEY']),
      ...mapActions([
        'FETCH_MY_SURVEY_FORM_TEST',
        'FETCH_MY_SURVEY_FORM',
        'REMOVE_MY_SURVEY'
      ]),
      
      noRedirectAnalysis() {
        swal("確認できません","誰も応じなかったです。","error", {button:"OK"});
      },
      surveyRemove() {
       swal({text: "本当に削除しますか？", icon: "warning", buttons: true, dangerMode: true})
      },
      albaCreateFormRoute() {
        this.$router.push({name: 'albaCreateForm'})
      }
    }
  }
</script>

<style scoped>
  .center_card {
    margin: 0 auto;
  }
  * {
    text-decoration: none;
  }
</style>