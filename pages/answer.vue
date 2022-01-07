<template>
  <v-app id="inspire">
    <v-main>
      <v-card>
        <v-container fluid>
          <v-row align="center" justify="center">
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
                  <span>{{ Get_DataStatePercentage }}</span>
                </div>
              </VueSvgGauge>
              <h2>تبریک ! شما ریسک پذیرید</h2>
            </v-col>
          </v-row>
          <div v-for="(item, index) in Get_Data" :key="index"></div>
        </v-container>

        <v-responsive :aspect-ratio="16 / 9">
          <v-container fluid>
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
            <div v-for="(item, index) in Get_Data" :key="index"></div>
          </v-container>
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
      return (100 / 4) * this.$store.getters.Get_reward.state + " %";
    },
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
