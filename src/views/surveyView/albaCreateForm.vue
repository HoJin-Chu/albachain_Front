<template>
  <div>
    <v-container fluid grid-list-md pt-5 mt-5>
       <v-form
        @submit.prevent="addAlbaForm"
        id="add-donation-form"
        enctype="multipart/form-data"
      >
        <v-layout row>
          <v-layout row wrap>
            <v-flex xs10>
              <div class="display-2 font-weight-bold pa-3 ml-5">
                <span class="grey--text text--darken-1">구인등록하기</span>
              </div>
            </v-flex>
            <v-flex xs2>
              <div class="mr-5 pa-3">
                <v-btn block color="info" type="submit" form="add-donation-form">
                  등록
                </v-btn>
            </div>
          </v-flex>
        </v-layout>
      </v-layout>
      <v-layout row wrap>
        <v-flex xs3 class="border_style">
          <v-card class="text-xs-center" flat style="background-color:#FAFAFA;" >
            <v-container fluid>
              <v-layout align-center justify-space-around column fill-height>
                <div class="headline font-weight-bold pt-5">고용주아이디</div>
                <div class="headline font-weight-bold pt-5 py-3">알바 시작일자</div>
                <div class="headline font-weight-bold pt-5 py-2">알바 기간</div>
                <div class="headline font-weight-bold py-5 my-5">정보</div>
              </v-layout>
            </v-container>
          </v-card>
        </v-flex>
        <v-flex xs9 class="border_style">
          <v-card  flat style="background-color:#FAFAFA;">
            <v-container fluid>
              <v-layout column fill-height>
                <div style="padding-top:3%">
                  <v-layout>
                    <v-flex xs5>
                      <v-text-field
                        v-model="title"
                        :rules="titleRules"
                        :counter="30"
                        label="아이디를 입력하세요"
                        required>
                      </v-text-field>
                    </v-flex>
                  </v-layout>
                </div>
                <div>
                  <v-flex xs3>
                      <v-menu
                        ref="menu"
                        v-model="menu"
                        :close-on-content-click="false"
                        :nudge-right="200"
                        lazy
                        offset-y
                        min-width="290px"
                      >
                        <template v-slot:activator>
                          <v-text-field
                            v-model="closed_at"
                            label="시작일"
                            prepend-icon="event"
                            readonly
                          ></v-text-field>
                        </template>
                        <v-date-picker
                          ref="picker"
                          v-model="closed_at"
                          max="2024-12-31"
                          min="2019-11-01"
                          @change="save"
                        ></v-date-picker>
                      </v-menu>
                    </v-flex>
                </div>
                <div class="py-4">
                  <v-layout>
                    <v-flex xs2>
                      <v-text-field type="number" v-model="target_amount" label="알바기간" required>
                      </v-text-field>
                    </v-flex>
                    <v-flex class="mt-4">시간</v-flex>
                  </v-layout>
                </div>
                <div class="py-4 my-3">
                  <v-flex xs5>
                    <v-textarea
                      v-model="content" solo
                      :rules="contentRules"
                      :counter="255"
                      label="설명"
                    >
                    </v-textarea>
                  </v-flex>
                </div>
              </v-layout>
            </v-container>
          </v-card>
        </v-flex>
      </v-layout>
      </v-form>
    </v-container>
  </div>
</template>

<script>
  import { mapActions, mapState }   from 'vuex'
  import { donation }               from '@/api/index'

  export default {
    computed: {
      ...mapState(['userinfo']),
    },
    data() {
      return {
        title:'',
        titleRules: [
          //모금함 이름 규격
          v => !!v || '내용을 입력하세요',
          v => v.length <= 30 || '30자 이내로 적어주세요'
        ],
        contentRules: [
          //모금함 설명 규격
          v => !!v || '정보를 적어주세요',
          v => v.length <= 255 || '255자 이내로 적어주세요'
        ],
        file:'',
        content:'',
        closed_at:null,
        target_amount:'',
        menu:false,
        // imageData: ""
        imageData: null,
      }
    },
    watch:{
      menu(val){
        val && setTimeout(() => (this.$refs.picker.activePicker = 'YEAR'))
      }
    },
    methods: {
      ...mapActions(['ADDDONATION','FETCH_DONATION','ADD_ALBA']),
      chooseImage () {
        this.$refs.fileInput.click()
      },
      onSelectFile () {
        const input = this.$refs.fileInput
        const files = input.files
        if (files && files[0]) {
          const reader = new FileReader()
          reader.onload = e => {
            this.imageData = e.target.result
          }
          reader.readAsDataURL(files[0])
          this.file = input.files[0]
        }
      },
      save (closed_at) {
        this.$refs.menu.save(closed_at)
      },
      adddonation() {
        let data = new FormData()
        data.append('user_id', this.userinfo.id)
        data.append('category',this.category)
        data.append('is_donator', this.userinfo.is_donator)
        data.append('title',this.title)
        data.append('file',this.file)
        data.append('content',this.content)
        data.append('closed_at', this.closed_at)
        data.append('target_amount',this.target_amount)
        let config = {
          headers : {
            'Content-Type' : 'multipart/form-data'
          }
        }
        this.ADDDONATION(data, config)
        this.$router.push({ name: 'donation' })
      },

      addAlbaForm() {
        let data = {
          'ID': this.title,
          'STARTDATE': this.closed_at,
          'ENDDATE': this.closed_at,
          'PAY': this.target_amount,
          'TEXT': this.content
        }
        // let data = new FormData()
        // data.append('ID', this.title)
        // data.append('STARTDATE', this.closed_at)
        // data.append('PERIOD', this.target_amount)
        // data.append('TEXT',this.content)
       
        this.ADD_ALBA(data)
        this.$router.push({ name: 'albaList' })
      },
    },
  }
</script>

<style scoped>
  .image-input {
    display: block;
    width: 260px;
    height: 260px;
    cursor: pointer;
    background-size: cover;
    background-position: center center;
  }
  .placeholder {
    background: #F0F0F0;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #333;
    font-size: 15px;
  }
  .placeholder:hover {
    background-color: #E0E0E0;
  }
  .file-input {
    display: none;
  }
  .border_style {
    border-bottom: 2px solid lightgrey;
    border-top: 2px solid lightgrey;
  }
  .border_style:nth-child(1) {
    border-right: 2px solid lightgrey;
  }
</style>