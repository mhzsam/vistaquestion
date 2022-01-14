<template>
  <v-app id="inspire">
    <v-main>
      <v-card>
        <v-container fluid>
          <v-row>
            <v-col class="col-4 mt-10" align="center" justify="center">
              <v-img class="mt-10" height="300" contain :src="img_src"></v-img>
              <strong> شما ریسک پذیرید</strong>
              <p>شما خود را سرمایه‌گذار محافظه کار معرفی کرده‌اید.

</p>
            </v-col>
            <v-col class="col-8 mt-5">
              <div >
                <div class="triangle-up hover_shape">
                 <span class="textline1"
                      ><ul>
                        <ol
                          v-for="(item, index) in offers1.reward"
                          :key="index"
                        >
                          {{
                            item.title
                          }}
                        </ol>
                      </ul></span
                    >
                </div>
                <div class="trapezoid1 hover_shape">
                  
                    <span class="textline2"
                      ><ul>
                        <ol
                          v-for="(item, index) in offers2.reward"
                          :key="index"
                        >
                          {{
                            item.title
                          }}
                        </ol>
                      </ul></span
                    >
          
                </div>
                <div class="trapezoid2 hover_shape">
                 <span class="textline3"
                      ><ul>
                        <ol
                          v-for="(item, index) in offers3.reward"
                          :key="index"
                        >
                          {{
                            item.title
                          }}
                        </ol>
                      </ul></span
                    >
                </div>
                <div class="trapezoid3 hover_shape">
                <span class="textline4"
                      ><ul>
                        <ol
                          v-for="(item, index) in offers4.reward"
                          :key="index"
                        >
                          {{
                            item.title
                          }}
                        </ol>
                      </ul></span
                    >
                </div>
              </div>
              <div id="container"></div>
            </v-col>
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
            <v-card-title class="justify-center mb-5">
              - پیشنهاد سبد گردانی ویستا -
            </v-card-title>
            <v-row>
              <v-col
                cols="6"
                sm="4"
                v-for="(item, index) in Get_Data"
                :key="index"
              >
                <v-img
                  height="200px"
                  :src="'data:image/jpeg;base64,' + item.reward.image"
                ></v-img>
                <v-card-title class="justify-center">{{
                  item.reward.title
                }}</v-card-title>

                <v-btn
                  block
                  elevation="2"
                  :href="'https://' + item.reward.link"
                >
                  {{ item.reward.link }}</v-btn
                >
                <br />
              </v-col>
            </v-row>
          </v-card>
        </v-container>

        <v-responsive :aspect-ratio="16 / 9">
          <v-container fluid> </v-container>
        </v-responsive>
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
      return (100 / 4) * this.$store.getters.Get_reward.state;
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
    if (resault == 25) {
      this.img_src = "img/25.png";
    } else if (resault == 50) {
      this.img_src = "img/50.png";
    } else if (resault == 75) {
      this.img_src = "img/75.png";
    } else if (resault == 100) {
      this.img_src = "img/100.png";
    } else {
      this.img_src = "img/25.png";
    }
    this.Get_DataForOffer();
  },
};
</script>
<style scoped>
.gauge {
  width: 25% !important;
}
.inner-text {
  padding-top: 40%;
  color: #87daad;
}
.textline1 {
  position: absolute;
  right: -18px;
  top: 45px;
  font-size: 13px;
  text-align: center !important;
  font-weight: bold;
   color: rgb(255, 255, 255);
}
.textline2 {
  position: absolute;
 right: 30px;
  top: 1px;
  font-size: 13px;
  text-align: center !important;
  font-weight: bold;
   color: white;
}
.textline3 {
  position: absolute;
 right: 85px;
  top: 40px;
  font-size: 13px;
  text-align: center !important;
  font-weight: bold;
   color: white;
}
.textline4 {
  position: absolute;
 right: 135px;
  top: 40px;
  font-size: 13px;
  text-align: center !important;
  font-weight: bold;
  color: white;
}
/* 
.line1 {
  position: absolute;
  top: 50px;
left: 0px;
  background-color: rgb(172, 171, 171);
  height: 5px;
  width: 200px;
}
.line2 {
  position: absolute;
  top: 50px;
left: 0px;
  background-color: rgb(172, 171, 171);
  height: 5px;
  width: 250px;
}
.line3 {
  position: absolute;
  top: 50px;
left: 0px;
  background-color: rgb(172, 171, 171);
  height: 5px;
  width: 300px;
}
.line4 {
  position: absolute;
  top: 50px;
left: 0px;
  background-color: rgb(172, 171, 171);
  height: 5px;
  width: 350px;
} */
.triangle-up {
  position: relative;
  margin: auto;
  width: 0;
  height: 0;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
  border-bottom: 100px solid #05e23e;
}

.trapezoid1 {
  position: relative;
  margin: auto;
  width: 200px;
  height: 0;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
  border-bottom: 100px solid #fdbb0e;
}
.trapezoid2 {
  position: relative;
  margin: auto;
  width: 300px;
  height: 0;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
  border-bottom: 100px solid #9852a1;
}
.trapezoid3 {
  position: relative;
  margin: auto;
  width: 400px;
  height: 0;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
  border-bottom: 100px solid #00a2e4;
}
.hover_shape:hover{
border-bottom-color: tomato !important;
}
</style>
