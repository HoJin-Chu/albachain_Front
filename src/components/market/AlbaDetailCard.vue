<template>
 <v-flex xs10 style="margin:0 auto;">
   
  <v-card color="#FAFAFA" style="cursor:pointer;" elevation="8" class="my-3 marketcard ">
    <v-layout align-center>
      <v-flex xs8>
        <v-card flat color="#FAFAFA">
          <div v-if="albaList.TEXT.length > 10" class="card-title 
          display-1 font-weight-bold pb-2">
          {{albaList.TEXT.substr(0,10) + "..."}}
          </div>

          <div v-else class="card-title 
          display-1 font-weight-bold pb-2">
          {{albaList.TEXT}}
          </div>
          <div class="card-text px-5 mx-5 font-weight-black">
          created By - {{albaList.NAME}}
          </div>
        </v-card>
      </v-flex>
      <v-flex xs3 text-xs-left>
        <v-card flat color="#FAFAFA" class="py-4 subheading font-weight-bold">
          <div class="headline font-weight-bold">
          \ <span class="info--text font-italic"> {{pay}} </span> 
          </div>
          <!-- <div>
            <i class="fas fa-user-alt">
              asd 人
            </i>
          </div> -->
          <div>
            <i class="far fa-calendar-alt font-weight-bold">
            {{start_date}}
           <!-- ~ {{end_date}} -->
            </i>
          </div>
        </v-card>
      </v-flex>
    </v-layout>
  </v-card>
 </v-flex>

</template>

<script>
  import { mapActions, mapState } from 'vuex'
  export default {
    name: 'AlbaDetailCard',
    props: ['albaList', 'index'],
    data() {
      return{
        pay: this.albaList.PAY || "미정",
        start_date: this.albaList.STARTDATE.substr(0,10) || "미정",
        // end_date: this.albaList.ENDDATE.substr(0,10) || "미정"
      }
    }
  }
</script>

<style scoped>
.marketcard{
  border-radius: 8px;
}

</style>
