<template>
  <div v-if="this.$route.name == 'surveymarket'">
         <v-img src="/static/alba_main.jpg" style="z-index:0; clip-path: ellipse(70% 90% at 48% 0%);"></v-img>
    <MarketJumbotron style="margin-top:-400px;"/>
    <MarketContext/>
  </div>
  <div v-else>
    <router-view/>
  </div>
</template>

<script>
  import MarketJumbotron from '@/components/market/MarketJumbotron'
  import MarketContext   from '@/components/market/MarketContext'

  export default {
    name: 'surveyMarket',
    components: {
      MarketJumbotron,
      MarketContext
    }
  }
</script>
