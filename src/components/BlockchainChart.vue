<template>
  <div class="blockchain">
    <LineChart :chartData="this.chartData"/>
    <ul v-for="(count, index) in pages" :key="index">
      <li @click="updateChart(count)">{{ index }}</li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import {LineChart} from 'vue-chart-3';
import {Chart, registerables} from 'chart.js';

Chart.register(...registerables);

export default {
  name: 'BlockchainChart',
  components: {
    LineChart
  },
  data() {
    return {
      chartData: null,
      pages: {'30d': 10, '60d': 20, '180d': 90, '1y': 122, '2y': 244, 'all': 0}
    }
  },
  methods: {
    async updateChart(count) {
      const response = await axios.get("http://localhost:8080/market-price.csv", {responseType: 'blob',});
      const file = response.data;
      file.text().then((csvStr) => {
        const data = csvStr.split('\n').slice(-count-2);
        let labels = [];
        let values = [];
        for (let i in data) {
          const elements = data[i].split(',');
          labels.push(elements[0]);
          values.push(elements[1]);
        }
        console.log(count);
        this.chartData = {
          labels,
          datasets: [
            {
              data: values
            },
          ],
        }
      });
    }
  },

  mounted() {
    this.updateChart();
  }
}
</script>

<style scoped>
</style>
