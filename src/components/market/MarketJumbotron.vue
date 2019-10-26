<template>
<div>
      <v-container fill-height>
        <v-layout align-center row wrap style="z-index:1">
          <v-flex xs12 style="text-align:center;">
            
            <div class="white--text page-title">
              알바를 한눈에 확인하세요 !

            </div>

            <div class="title white--text">
              나의 정보를 안전하게 AlbaChain.
            </div>
          </v-flex>
        </v-layout>
      </v-container>
  </div>
</template>
<script>
  import { mapMutations, mapState, mapActions }   from 'vuex'
  
  export default {
    name:'maketJumbotron',
    methods: {
      ...mapMutations([ 'SET_IS_SURVEY_SALE' ])
    },
    
	}
</script>

<style scoped>

  .page-title{
    font-size:3em;
    font-weight: bold;
    text-shadow: 2px 2px 4px #00000048;
  }

  .sell-but{
    padding-top:20px;
    padding-bottom:40px;
    border-radius: 50px
  }
</style>