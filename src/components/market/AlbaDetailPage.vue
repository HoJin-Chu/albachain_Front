/* 구매 설문 상세정보 */
<template lang="html">
<v-container grid-list-xs fluid style="margin-top:100px;">
  
  <v-layout>
    <v-flex xs3 class="border_style">
      <v-card class="text-xs-center" flat style="background-color:#FAFAFA;" >
        <v-container fluid>
          <v-layout align-center justify-space-around column fill-height>
            <div class="display-1 font-weight-bold my-5 py-5">아르바이트 정보</div>
            <div class="display-1 font-weight-bold py-5 my-5">????</div>
          </v-layout>
        </v-container>
      </v-card>
    </v-flex>
    <v-flex xs9 class="border_style">
      <v-card flat style="background-color:#FAFAFA;">
        <v-container fluid>
          <v-layout column fill-height>
            <div>
              <div class="title font-weight-bold px-4 pt-4 mt-2 pb-5">제목
                <span class="pl-5 ml-5 subheading grey--text">텍스트</span>
              </div>
              <div class="title font-weight-bold px-4 pb-3">
                <v-tooltip right color="info">
                  <span slot="activator">
                    <i class="far fa-calendar-alt ma-1"></i>
                    <span>asdas</span>
                    ~ asdasd
                    </span>
                  </span>
                  <span>進行日程</span>
                </v-tooltip>
              </div>
              <div class="title font-weight-bold px-4 pb-3">
                <v-tooltip right color="info">
                  <span slot="activator">
                    <i class="fas fa-coins ma-1"></i><span>asda</span> 원
                  </span>
                  <span>販売価格</span>
                </v-tooltip>
              </div>
              
              <div  class="px-3">
                <v-chip class="pa-1" color="grey darken-2" text-color="white" large close>すべての人数</v-chip>
              </div>
            </div>
            <div style="margin-top:50px;">
           
            </div>
          </v-layout>
        </v-container>
      </v-card>
    </v-flex>
  </v-layout>
</v-container>

</template>

<script>
  import MarketDetailItem from './MarketDetailItem'

  export default {
    components: { MarketDetailItem },
    props:['marketItems','ino'],
    filters:{
      substr:function(date){
        if(date){
          return date.substr(0,10)
        }
      }
    },
    mounted: {
     
    },
    methods: {
      
    },
  }
</script>
<style scoped>
  .border_style {
    border-bottom: 2px solid lightgrey;
    border-top: 2px solid lightgrey;
  }
  .border_style:nth-child(1) {
    border-right: 2px solid lightgrey;
  }
  .questions{
    font-size: 1.4em;
    border: 1px solid #bbbbbb;
    border-radius: 10px;
  }
  .circle{
    border:1px solid grey;
    border-radius:50%;
  }
</style>
