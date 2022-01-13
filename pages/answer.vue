<template>
  <v-app id="inspire">
    <v-main>
      <v-card>
        <v-container fluid>
          <v-row>
            <v-col class="col-4" align="center" justify="center">
              <v-img height="300" contain :src="img_src"></v-img>
              <strong> شما ریسک پذیرید</strong>
            </v-col>
            <v-col class="col-8">
              <div class="triangle-up"></div>
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
            <v-card-title class="justify-center mb-5">  پیشنهاد سبد گردانی ویستا </v-card-title>
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
</style>
