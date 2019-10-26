/* 네비게이션 */

<template>
  <v-toolbar 
    v-scroll="onScroll" app :flat="!isScrolling"
    :color="!isScrolling ? 'transparent' : '#FFFFFF'"
    style="z-index: 9999; "
    >
    <router-link to="/">
      <h1 style="font-size:40px;" class="pa-4">AlbaChain</h1>
    </router-link>
    <v-toolbar-items v-if="$vuetify.breakpoint.mdAndUp && this.$route.name == 'home'">
      <!-- :active-class="!isScrolling ? 'grey--text text--darken-3' : 'grey--text text--darken-3'"  -->
      <v-btn
        v-for="(item,i) in items" :key="i" :to="item.to" flat 
        :class="!isScrolling ? 'title white--text' : 'title grey--text text--darken-3'">
          <span v-text="item.text"/>
      </v-btn>
    </v-toolbar-items>
    <v-toolbar-items v-if="$vuetify.breakpoint.mdAndUp && this.$route.name !== 'home'">
      <v-btn
        v-for="(item,i) in items" :key="i" :to="item.to" flat 
        :class="!isScrolling ? 'title grey--text text--darken-3' : 'title grey--text text--darken-3'">
          <span v-text="item.text"/>
      </v-btn>
    </v-toolbar-items>
    <v-spacer/><v-spacer/><v-spacer/><v-spacer/><v-spacer/><v-spacer/><v-spacer/><v-spacer/><v-spacer/><v-spacer/>
    <template v-if="!isAuth">
      <v-btn v-if="$vuetify.breakpoint.mdAndUp"  :active-class="!isScrolling ? 'blue--text' : undefined" @click="SET_IS_LOGIN(true)" flat  class="subheading"><span style="font-size:18px;">로그인</span></v-btn>
      <v-btn v-if="$vuetify.breakpoint.mdAndUp"  :active-class="!isScrolling ? 'blue--text' : undefined" :to="{name : 'join'}" flat  class="subheading"><span style="font-size:18px;">회원가입</span></v-btn>
    </template>
    <template v-else>
      <v-btn v-if="$vuetify.breakpoint.mdAndUp"  :active-class="!isScrolling ? 'blue--text' : undefined" :to="{name : 'mypage'}" flat class="subheading"><span style="font-size:18px;">마이페이지</span></v-btn>
      <v-btn v-if="$vuetify.breakpoint.mdAndUp"  :active-class="!isScrolling ? 'blue--text' : undefined" 
      @click.prevent="logout" flat class="subheading"><span style="font-size:18px;">로그아웃</span></v-btn>
    </template>
    <v-spacer/>

    <v-btn v-if="!$vuetify.breakpoint.mdAndUp" icon @click="toggleDrawer">
      <v-icon color="blue">menu</v-icon>
    </v-btn>
  </v-toolbar>
</template>

<script>
  import { mapMutations, mapGetters } from 'vuex'
  import { setAuthInHeader } from '../api';

  export default {
    data(){
      return{
        isScrolling: false,
      }
    },
    computed: {
      // isAuth Test Token
      ...mapGetters(['isAuth']),
      items () {
        return this.$t('View.items')
      },
    },
    methods: {
      ...mapMutations([
        'SET_IS_LOGIN', 
        'LOGOUT',
        'toggleDrawer',  
      ]),
      logout() {
        swal({
          text: "ログアウトしますか？",
          icon: "warning",
          buttons: true,
          dangerMode: true,
        })
        .then((willDelete) => {
          if (willDelete) {
            swal("ログアウトしました！");
            this.LOGOUT()
            this.$router.push({name:'home'})
          }
        });
      },
      onScroll () {
        this.isScrolling = (window.pageYOffset || document.documentElement.scrollTop || 0) > 60
      }
    }
  }
</script>