<template>
  <div>
    <v-app  class="app-setup" >
      <div >

      
      <v-stepper class="padding" v-model="e1">
        <v-stepper-items v-for="(item, index) in Get_Data" :key="index">
          <v-stepper-content class="pb-0 mb-n8" :step="index + 1">
            <v-card
              class="pt-0 mt-0 mx-3"
              color="white "
              height="auto"
              padding="20px"
              elevation="0"
            >
              <v-container class="pt-0 mt-0 pb-0" fluid>
                <v-card-title
                  primary-title
                  class="pb-0 pt-0 goldcolor justify-center"
                >
                  ارزیابی ریسک
                </v-card-title>
                <v-radio-group v-model="radioGroup">
                  <template>
                    <div style="font-size: 16px; color: black">
                      <p>{{ item.question_text }}</p>
                    </div>
                  </template>
                  <v-radio
                    class="radiogroup"
                    active-class="radiogroupactive"
                    color="green"
                    v-for="(item2, index2) in item.answer2"
                    :key="index2"
                    :label="item2.answer_text"
                    :value="parseInt(item2.answer_score)"
                    :on-icon="'mdi-checkbox-marked-circle'"
                    :off-icon="'mdi-checkbox-blank-circle-outline'"
                  ></v-radio>
                </v-radio-group>
                <!-- 
                <v-list>
                  <v-list-item-group v-model="radioGroup" color="green">
                    <template>
                      <div style="font-size: 16px; color: black">
                        <p>{{ item.question_text }}</p>
                      </div>
                    </template>
                    <v-list-item
                      v-for="(item2, index2) in item.answer2"
                      :key="index2"
                      :label="item2.answer_text"
                      :value="parseInt(item2.answer_score)"
                    >
                      <v-list-item-icon>
                        <v-icon>{{ icon }}</v-icon>
                      </v-list-item-icon>
                      <v-list-item-content>
                        <v-list-item-title
                          v-text="item2.answer_text"
                        ></v-list-item-title>
                      </v-list-item-content>
                    </v-list-item>
                  </v-list-item-group>
                </v-list> -->
              </v-container>

              <v-container fluid px-10>
                <v-row class="d-flex justify-space-between mb-6">
                  <div>
                    <v-btn
                      class="btn-bold btn-back"
                      color="#666666"
                      @click="resetSumOfRadio(index)"
                      width="150"
                    >
                      بازگشت
                    </v-btn>
                  </div>
                  <v-row class="d-flex justify-center pt-4">
                    <div
                      v-for="(item, index) in Get_Data"
                      :key="index"
                      class="shape-botton"
                      :id="index + 1"
                      :class="{shapebotton:(index+1)>=e1,shapeactive:(index+1)==e1,shapeback:(index+1)<e1}"
                      
                    ></div>
                  </v-row>
                  <div>
                    <v-btn
                      v-if="index !== Get_Data.length - 1"
                      class="btn-bold btn-next"
                      width="150"
                      color="#B29353"
                      @click="sumAllOfRadio(index)"
                    >
                      <!-- e1 = index + 2; -->
                      بعدی
                    </v-btn>
                    <v-btn
                      v-if="index == Get_Data.length - 1"
                      color="#B29353"
                      @click="sumAllOfRadioAnd()"
                      width="150"
                      class="btn-next"
                    >
                      ثبت
                    </v-btn>
                  </div>
                </v-row>
              </v-container>
            </v-card>
          </v-stepper-content>
        </v-stepper-items>
        <v-row class="d-flex justify-center mt-n1 pb-5 pt-0">
          <div class="step_counter" style="color: #b29353">{{ e1 }}</div>
          <div class="step_counter">|</div>
          <div class="step_counter" style="color: #173245">{{ allPage }}</div>
        </v-row>
      </v-stepper>
      </div>
    
    </v-app>
    <!-- <div v-for="item in contents" :key="index">
    {{item.}}
    </div> -->
  </div>
</template>

<script>
export default {
  name: "question",

  data() {
    return {
      isActive: false,
      isActive2: false,

      correctPage: 0,
      allPage: 0,
      icon: "mdi-checkbox-blank-circle-outline",
      e1: 1,
      radioGroup: 0,
      sumOfRadio: 0,
      lastRadioValue: [],
      reqest: false,
      contents: [],
    };
  },
  // async fetch() {
  //   await  this.$store.dispatch("FetchData");
  // },
  asyncData({ store }) {
    return store.dispatch("FetchData");
  },

  computed: {
    //   async fetch() {
    //   await  this.$store.dispatch("FetchData");
    // },
    Get_Data() {
      return this.$store.getters.Get_Data.data;
    },
  },
  mounted() {
    this.allPage = this.Get_Data.length;
  },
  methods: {
    sumAllOfRadio(index) {
      if (this.radioGroup != 0) {
        this.lastRadioValue.push(this.radioGroup);
        // console.log(" this.lastRadioValue", this.lastRadioValue);
        this.sumOfRadio = this.radioGroup + this.sumOfRadio;
        console.log("sum is", this.sumOfRadio);
        this.radioGroup = 0;
        this.e1 = index + 2;
      } else {
        alert("لطفا یک مقدار را انتخاب کنید");
      }
    },
    resetSumOfRadio(index) {
      if (index !== 0) {
        var last = this.lastRadioValue.at(-1);
        this.lastRadioValue.pop();
        // console.log("lastRadioValue",this.lastRadioValue)
        // console.log("last",last)
        this.sumOfRadio = this.sumOfRadio - last;
        var setp = index + 1;
        this.e1 = setp - 1;
        console.log("sum is", this.sumOfRadio);
      } else {
        alert("شما در مرحله اول هستید ");
      }
    },
    sumAllOfRadioAnd() {
      this.sumAllOfRadio();
      var param = this.sumOfRadio;
      // console.log("param", param);
      this.$store.dispatch("FetchReward", param);
    },
  },
};
</script>
<style scoped>
.app-setup{
 height: 420px;



}
.padding{
  padding: 0 10%
}
.btn-bold {
  font-weight: bold !important;
}
* {
  text-align: right !important;
}
.text_box {
  padding: 5px 50px;
}
.text_box p {
  text-align: justify !important;
}
.goldcolor {
  color: #b19355;
  font-size: 20px;
  font-weight: 600;
}
.radiogroup {
  padding: 8px;
  border-radius: 20px;
  border: 1px solid rgb(214, 214, 214) !important ;
}
.radiogroupactive {
  padding-top: 10px;
  padding-bottom: 10px;
  border-radius: 50px;
  border: 1px solid rgb(189, 189, 189) !important ;
  box-shadow: 0px 1px 2px gray;
}
.btn-back {
  color: white;
  border-radius: 50px !important;
}
.btn-next {
  color: white !important;
  border-radius: 50px !important;
}
.shapebotton {
  background-color: #eeeeee;
  height: 10px;
  width: 30px;
  border: 1px #eeeeee solid;
  border-radius: 5px;
  margin-left: 3px;
  margin-right: 3px;
  margin-top: 12px;
}
.shapeactive{
background-color: #b19355;
  height: 10px;
  width: 30px;
  border: 1px #b19355 solid;
  border-radius: 5px;
  margin-left: 3px;
  margin-right: 3px;
  margin-top: 12px;
}
.shapeback{
background-color: #173245;
  height: 10px;
  width: 30px;
  border: 1px #173245 solid;
  border-radius: 5px;
  margin-left: 3px;
  margin-right: 3px;
  margin-top: 12px;
}
.step_counter {
  margin-left: 5px;
  margin-right: 5px;
}
</style>
