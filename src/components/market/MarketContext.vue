<template>
  <span>
    <v-container fluid grid-list-xl v-if="!this.$store.state.loading">
      <v-layout text-xs-center row wrap class="pa-2 mx-5">
        <v-layout row wrap justify-center>
          <v-flex xs12 v-for="(albaList, index) in myAlbaForm.jobOffer" :key="index">
            <router-link
              :to="{
                name: 'AlbaDetailPage',
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
  </span>
</template>

<script>
  import { mapActions, mapState }    from 'vuex'
  import Spinner2                    from '@/components/Spinner2'
  import AlbaDetailCard              from '@/components/market/AlbaDetailCard'

  export default {
    name:'MarketContext',
    components: { Spinner2, AlbaDetailCard },
    data(){
      return{
        search:'',
        }
    },
    computed: {
      ...mapState([ 'saleSurvey', 'userinfo', 'myAlbaForm']),
    },
    mounted() {
      this.FETCH_ALBA()
    },
    methods: {
      ...mapActions(['FETCH_ALBA']),
    }
  }
</script>