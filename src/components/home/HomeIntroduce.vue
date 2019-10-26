<template lang="html">
  <v-fade-transition mode="out-in">
    <v-layout column>

      <v-flex xs12 id="element">
        <div
          class="pa-5"
          data-aos="fade-right"
          data-aos-delay="200" >
          <v-layout row　align-center justify-center>
          <span class="text-xs-left text-md-left ">
            <span class="headline info--text text-xs-left font-weight-black">고용주</span>
            <div class="mt-4 title message" >
              편하게 근로계약서를 작성하고<br>
              업무 집중도 상승시켜 보세요.
            </div>
          </span>
          <v-img src="/static/소상공인.png" class="ma-5" max-width="15%"></v-img>
          </v-layout>
        </div>
      </v-flex>
      <v-flex xs12>
        <div
          class="pa-5"
          data-aos="fade-right"
          data-aos-delay="200"
          >
          <v-layout  align-center justify-center>
              <v-img src="/static/알바.png" class="ma-5" max-width="15%" centered></v-img>
              <span class="text-xs-left text-md-left ">
                <span class="headline info--text text-xs-left font-weight-black">피고용자</span>
                <div class="mt-4 title message" >
                  안전하게 근로계약서를 작성하고<br>
                  심리적인 불안감을 해소하세요.
                </div>
              </span>
          </v-layout>
        </div>
      </v-flex>
      <!-- ino 설명 추가하기  -->
      <v-flex md12 text-md-center text-xs-center>
        <v-img src="/static/background.png">
        <div
          height="30vh"
          class="pa-5 mt-5"
          data-aos="flip-up"
          data-aos-delay="200" >
          <v-card-text class="display-2 mt-5">
             Albachain을 이용해 보시겠습니까?
          </v-card-text>
        </div>
        </v-img>
      </v-flex>
    </v-layout>
  </v-fade-transition>
</template>

 <style scoped>
.message {
  line-height: 200%;
}
</style>