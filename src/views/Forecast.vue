<template>
  <div class="forecast">
    <div class="forecast-block">
      <p class="forecast-label">Temperature</p>
      <v-chart :options="temperature" />
    </div>
    <div class="forecast-block">
      <p class="forecast-label">Pressure</p>
      <v-chart :options="pressure" />
    </div>
    <div class="forecast-block">
      <p class="forecast-label">Humidity</p>
      <v-chart :options="humidity" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import ECharts from "vue-echarts";
import "echarts/lib/chart/line";

export default {
  components: {
    "v-chart": ECharts
  },

  data() {
    return {
      temperature: {
        xAxis: {
          type: "category",
          data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
        },
        yAxis: {
          type: "value",
          name: "Celcius"
        },
        series: [
          {
            data: [24, 27, 28, 26, 30, 32, 25],
            type: "line"
          }
        ],
        animationDuration: 1000
      },
      pressure: {
        xAxis: {
          type: "category",
          data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
        },
        yAxis: {
          type: "value",
          name: "mmHg"
        },
        series: [
          {
            data: [680, 700, 640, 720, 710, 680, 690],
            type: "line"
          }
        ],
        animationDuration: 1000
      },
      humidity: {
        xAxis: {
          type: "category",
          data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
        },
        yAxis: {
          type: "value",
          name: "%"
        },
        series: [
          {
            data: [74, 70, 65, 60, 80, 62, 68],
            type: "line"
          }
        ],
        animationDuration: 1000
      }
    };
  },

  async beforeCreate() {
    const APIKey = "9d8ba6f4b0f385d05fb3f3caa77e1902";
    const instance = axios.create({
      baseURL: "http://pro.openweathermap.org/data/2.5"
    });
    try {
      const response = await instance({
        method: "get",
        url: `/forecast/hourly?q=${this.$route.params.city}&appid=${APIKey}`
      });
      console.log(response);
    } catch (error) {
      console.error(error);
    }
  }
};
</script>

.<style lang="scss">
.forecast {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.forecast-block {
  border: solid 1px #7fdbff;
  margin: 1rem 0;
  padding: 1rem;
  border-radius: 0.2rem;
}
</style>
