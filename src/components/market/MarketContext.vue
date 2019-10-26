<template>
  <span>
    <v-container fluid grid-list-xl v-if="!this.$store.state.loading">
      <v-layout text-xs-center row wrap class="pa-2 mx-5">
        <v-layout row wrap justify-center>
          <v-flex xs12 v-for="(albaList, index) in myAlbaForm" :key="index">
            <router-link
              :to="{
                name: 'AlbaDetailCard',
                params:{ albalist_id: albaList._id}
              }">
                <AlbaDetailCard
                :albaList="albaList"
                :index="index"
                />
            </router-link>
          </v-flex>
        </v-layout>
      </v-layout>
    </v-container>
    <Spinner2 v-else/>
    <surveySale
    :userinfo="userinfo"
    />
  </span>
</template>

<script>
  import { mapActions, mapState }    from 'vuex'
  import MarketCard                  from '@/components/market/MarketCard'
  import Spinner2                    from '@/components/Spinner2'
  import surveySale                  from '@/components/dialog/surveySale'
  import AlbaDetailCard              from '@/components/market/AlbaDetailCard'

  export default {
    name:'MarketContext',
    components: { MarketCard, Spinner2, surveySale, AlbaDetailCard },
    data(){
      return{
        search:'',
        items:[
          { text: 'すべて', value:1 },
          { text: 'タイトル', value:2 },
          { text: '紹介文', value:3 },
          ]
        }
    },
    computed: {
      ...mapState([ 'saleSurvey', 'userinfo', 'myAlbaForm']),
      surveyList() {
        var sellingSurvey = this.saleSurvey.filter((card) => {
          if(this.items.value == 2){
            return card.title.toLowerCase().includes(this.search.toLowerCase())
          }
          else if(this.items.value ==3){
            return card.description.toLowerCase().includes(this.search.toLowerCase())
          }
          else{
            return card.title.toLowerCase().includes(this.search.toLowerCase())||card.description.toLowerCase().includes(this.search.toLowerCase())
          }
        })
        return sellingSurvey.sort((x,y) => { return y.id - x.id})
      }
    },
    mounted() {
      this.FETCH_MARKET({ id: this.userinfo.id })
      this.FETCH_ALBA()
    },
    methods: {
      ...mapActions(['FETCH_MARKET', 'FETCH_ALBA']),
    }
  }
</script>