
  <template>
  <div>
    <v-app id="inspire">
      <v-stepper v-model="e1">
        <v-stepper-header>
          <div v-for="(item, index) in Get_Data" :key="index">
            <v-stepper-step :complete="e1 > index + 1" :step="index + 1">
              سوال {{ index + 1 }}
            </v-stepper-step>
          </div>
          <!-- <v-stepper-step :complete="e1 > 2" step="2"> </v-stepper-step>
          <v-divider></v-divider> -->
        </v-stepper-header>

        <v-stepper-items v-for="(item, index) in Get_Data" :key="index">
          <v-stepper-content :step="index + 1">
            <v-card
              class="mb-12 ma-3"
              color="grey lighten-4"
              height="auto"
              padding="20px"
            >
              <v-container class="px-10" fluid>
                <v-radio-group v-model="radioGroup">
                  <template #label>
                    <div>
                      <h2>{{ item.question_text }}</h2>

                      <br />
                    </div>
                  </template>
                  <v-radio
                    v-for="(item2, index2) in item.answer2"
                    :key="index2"
                    :label="item2.answer_text"
                    :value="parseInt(item2.answer_score)"
                  ></v-radio>
                </v-radio-group>
              </v-container>
            </v-card>

            <v-btn
              v-if="index !== Get_Data.length - 1"
              class="btn-bold right"
              right
              color="primary"
              @click="
                sumAllOfRadio();
                e1 = index + 2;
              "
            >
              بعدی
            </v-btn>
            <v-btn
              v-if="index !== 0"
              class="btn-bold align "
              color="error"
              
              outlined
              @click="
                resetSumOfRadio();
                e1 = 1;
              "
            >
              بازگشت 
            </v-btn>
            <v-btn
           
              v-if="index == Get_Data.length - 1"
              color="primary"
              @click="sumAllOfRadioAnd()"
            >
              ارسال
            </v-btn>
          </v-stepper-content>

          <!-- 
          <v-stepper-content step="2">
            <v-card class="mb-12" color="grey lighten-4" height="200px"
              ><v-container class="px-10" fluid>
                <v-radio-group v-model="radioGroup">
                  <template #label>
                    <div>
                      <h2>{{ question2 }}</h2>
                      <br />
                    </div>
                  </template>
                  <v-radio
                    v-for="n in 3"
                    :key="n"
                    :label="`Radio ${n}`"
                    :value="n"
                  ></v-radio>
                </v-radio-group>
              </v-container>
            </v-card>

            <v-btn class="btn-bold" color="primary" @click="e1 = 1">
              ارسال
            </v-btn>

            <v-btn class="btn-bold" text @click="e1 = 1"> قبلی </v-btn>
          </v-stepper-content> -->
        </v-stepper-items>
        <div class="text_box">
      <h3>با ما، سرمایه‌گذار شو!</h3>
      <p> از طریق این اپلیکیشن، شما می‌توانید در انواع صندوق‌های سکه طلا، درآمد ثابت با سود روزشمار و سهامی ثبت نام کرده و سرمایه‌گذاری کنید. کیان دیجیتال متعلق به گروه مالی کیان و محصول مشترک شرکت مشاور سرمایه‌گذاری پرتو آفتاب کیان، کارگزاری توسعه معاملات کیان و شرکت نوآوران پذیرش پیشرو کیان است. مشاور سرمایه‌گذاری پرتو آفتاب کیان جز نهادهای مالی ثبت شده در سازمان بورس با شماره ثبت ۱۱۵۴۳ و شماره مجوز ۱۲۱/۸۵۲۸۸ برای مشاوره سرمایه‌گذاری است. همچنین کارگزاری توسعه معاملات کیان ثبت شده به شماره ۱۰۶۷۳ نزد سازمان بورس و اوراق بهادار و دارای شماره مجوز ۱۲۱/۹۹۰۰۳ برای انجام معاملات برخط است. شرکت نوآوران پذیرش پیشرو کیان نیز دارای مجوز پرداخت‌یاری از سوی شرکت شاپرک بانک مرکزی است. صندوق‌های سرمایه‌گذاری کیان دیجیتال تحت مدیریت مشاور سرمایه‌گذاری پرتو آفتاب کیان و دارای مجوز از سازمان بورس و اوراق بهادار بوده و تحت نظارت و پایش مستمر این سازمان فعالیت می‌کنند. در سایت نهادهای مالی ثبت شده در سازمان بورس این مجوزها را می‌توانید مشاهده کنید (cfi.codal.ir). کیان دیجیتال دارای تائیدیه از مرکز نظارت بر امنیت اطلاعات بازار سرمایه به شماره ۱۲۱/۱۳۵۴۹۶ است.</p>
        </div>
      </v-stepper>
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
      e1: 1,
      radioGroup: 0,
      sumOfRadio: 0,
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
  methods: {
    sumAllOfRadio() {
      this.sumOfRadio = this.radioGroup + this.sumOfRadio;
      console.log(this.sumOfRadio);
      this.radioGroup=0
    },
    resetSumOfRadio() {
      this.sumOfRadio = 0;
      console.log("sum is", this.sumOfRadio);
    },
    sumAllOfRadioAnd() {
      this.sumAllOfRadio();
      var param = this.sumOfRadio;
      console.log("param", param);
      this.$store.dispatch("FetchReward", param);
    },
  },
};
</script>
<style scoped >

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

</style>