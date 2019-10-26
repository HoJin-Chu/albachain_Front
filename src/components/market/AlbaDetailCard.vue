<template>
  <v-card color="#FAFAFA" style="cursor:pointer;" elevation="8" class="my-3 marketcard">
    <v-layout align-center>
      <v-flex xs9>
        <v-card flat color="#FAFAFA">
          <div class="card-title 
          display-1 font-weight-bold pb-2">
          {{albaList}}
          </div>
          <div class="card-text px-5 mx-5 font-weight-black">
          asd
          </div>
        </v-card>
      </v-flex>
      <v-flex xs3 text-xs-left>
        <v-card flat color="#FAFAFA" class="py-4 subheading font-weight-bold">
          <div class="headline font-weight-bold">
           <span class="info--text font-italic"> asd </span> INO
          </div>
          <div>
            <i class="fas fa-user-alt">
              asd 人
            </i>
          </div>
          <div>
            <i class="far fa-calendar-alt font-weight-bold">
            asd
            ~ asd
            </i>
          </div>
        </v-card>
      </v-flex>
    </v-layout>
  </v-card>
</template>

<script>
  import { mapActions, mapState } from 'vuex'
  export default {
    name: 'AlbaDetailCard',
    props: ['albaList', 'index'],
  }
</script>

<style scoped>
.marketcard{
  border-radius: 8px;
}
</style>
