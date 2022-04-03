<template>
  <v-app class="app-setup">
    <v-main>
      <v-card>
        <v-container fluid>
          <v-row>
            <v-col class="col-4 mt-10" align="center" justify="center"> </v-col>

            <v-col class="col-4 mt-10">
              <h2 style="color: #b19355" align="center" justify="center">
                نتیجه ارزیابی ریسک
              </h2>
              <v-img class="mt-10" height="300" contain :src="img_src"></v-img>
              <br />
              <div class="mr-5">
                <h2>
                  شما <span style="color: #b19355">نسبتا ریسک پذیر</span> هستید
                </h2>
                <br />
                <span style="font-size: 1.2em">
                  سهام رشدی (دارای پتانسیل سودآوری در آینده و فاقد سود تقسیمی)
                </span>
                <br />
                <span style="font-size: 1.2em"
                  >سهام ارزشی ( قیمت معاملاتی پایین تر از ارزش ذاتی)</span
                >
              </div>
            </v-col>
            <v-col class="col-4 mt-10" align="center" justify="center"> </v-col>
          </v-row>
          <!-- <v-row align="center" justify="center">
            <v-col align="center" justify="center" class="gauge">
              <br />
              <VueSvgGauge
                :start-angle="-90"
                :end-angle="90"
                :value="Get_DataState"
                :separator-step="1"
                :min="0"
                :max="4"
                :gauge-color="[
                  { offset: 0, color: '#347AB0' },
                  { offset: 100, color: '#8CDFAD' },
                ]"
                :scale-interval="0.1"
              >
                <div class="inner-text">
                  <span>{{ Get_DataStatePercentage }} %</span>
                </div>
              </VueSvgGauge>
              <h2>تبریک ! شما ریسک پذیرید</h2>
            </v-col>
          </v-row> -->
          <v-card class="mt-10">
            <v-card-title
              style="color: #b19355; font-weight: 550"
              class="justify-center mb-5 text-h4 mb-12 pt-12"
            >
              پیشنهاد ویستا
            </v-card-title>
            <v-row
              class="d-flex justify-center"
              style="margin-left: 18%; margin-right: 18%"
            >
              <v-col
                cols="6"
                sm="4"
                v-for="(item, index) in Get_Data"
                :key="index"
              >
                <v-img
                 class="mx-12"
                  :src="'data:image/jpeg;base64,' + item.reward.image"
                ></v-img>
                <!-- <v-img class="mx-12" src="/img/1.png"></v-img> -->
                <v-card-title class="justify-center">{{
                  item.reward.title
                }}</v-card-title>
                <v-card-text
                  style="font-size: 1.1em; line-height: 1.6"
                  class="text-justify"
                >
                  تمامی تلاش مدیریت، کارشناسان و کارکنان سبدگردانـی ویستا معطوف
                  به ارایه خدمات به مشتریان براساس سه اصل اعتماد، اطمینان و حرفه
                  ای گری است
                </v-card-text>
                <!-- <v-btn
                  block
                  elevation="2"
                  :href="'https://' + item.reward.link"
                >
                  {{ item.reward.link }}</v-btn
                > -->
                <br />
              </v-col>
            </v-row>
            <v-row>
              <v-btn
                large
                style="color: white"
                color="#B29353 "
                elevation="2"
                class="btn pt-0 mt-n10"
                >شروع سرمایه گذاری
              </v-btn>
              <br />
            </v-row>
          </v-card>
        </v-container>

       
      </v-card>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "answer",
  data() {
    return {
      img_src: "",
      rewards: [],
      offers1: [],
      offers2: [],
      offers3: [],
      offers4: [],
      percentage: (100 / 4) * 4 + " %",
    };
  },
  computed: {
    Get_Data() {
      return this.$store.getters.Get_reward.data;
    },
    Get_DataState() {
      return this.$store.getters.Get_reward.state;
    },
    Get_DataStatePercentage() {
      return  this.$store.getters.Get_reward.state;
    },
  },
  methods: {
    Get_DataForOffer() {
      return this.$axios({
        method: "get",
        url: "http://vistaapi.citnog.ir/api/v1/customer/question/reward_all/",
      })
        .then((response) => {
          console.log("res", response.data);
          var data = response.data;
          this.offers1 = data[0];
          this.offers2 = data[1];
          this.offers3 = data[2];
          this.offers4 = data[3];
        })
        .catch((err) => {
          console.log("err");
        });
    },
  },
  mounted() {
    var resault = this.Get_DataStatePercentage;
    if (resault === 1) {
      this.img_src = "img/20.png";
    } else if (resault === 2) {
      this.img_src = "img/40.png";
    } else if (resault === 3) {
      this.img_src = "img/60.png";
    } else if (resault === 4) {
      this.img_src = "img/80.png";
    } else if (resault === 5) {
      this.img_src = "img/100.png";
    } else {
      this.img_src = "img/20.png";
    }
    this.Get_DataForOffer();
  },
};
</script>
<style scoped>
.btn {
  display: inline-block;
  margin: 20px auto;
  font-size: 1.3em;
  color: white !important;
  border-radius: 50px !important;
}
</style>
