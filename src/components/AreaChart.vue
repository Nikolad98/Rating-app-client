<template>
  <div>
    <canvas ref="canvas" class="areaChart"></canvas>
  </div>
</template>
<script>
import { Line } from 'vue-chartjs';

export default {
  extends: Line,
  props: ['hours', 'values', 'names'],
  data() {
    return {
      gradient: [],
      colors: [],
      array: [],
      smiles: this.names,
    };
  },
  methods: {
    createGraf() {
      this.gradient0 = this.$refs.canvas.getContext('2d').createLinearGradient(0, 0, 0, 400);
      this.gradient1 = this.$refs.canvas.getContext('2d').createLinearGradient(0, 0, 0, 400);
      this.gradient2 = this.$refs.canvas.getContext('2d').createLinearGradient(0, 0, 0, 400);
      this.gradient3 = this.$refs.canvas.getContext('2d').createLinearGradient(0, 0, 0, 400);
      this.gradient4 = this.$refs.canvas.getContext('2d').createLinearGradient(0, 0, 0, 400);

      this.gradient0.addColorStop(0, 'rgba(4, 210,124, 0.4)');
      this.gradient0.addColorStop(0.5, 'rgba(4, 210,124, 0.12)');
      this.gradient0.addColorStop(1, 'rgba(4, 210,124, 0)');

      this.gradient1.addColorStop(0, 'rgba(65, 179, 233, 0.4)');
      this.gradient1.addColorStop(0.5, 'rgba(65, 179, 233, 0.12)');
      this.gradient1.addColorStop(1, 'rgba(65, 179, 233, 0)');

      this.gradient2.addColorStop(0, 'rgba(176, 176, 178, 0.4)');
      this.gradient2.addColorStop(0.5, 'rgba(176, 176, 178, 0.12)');
      this.gradient2.addColorStop(1, 'rgba(176, 176, 178, 0)');

      this.gradient3.addColorStop(0, 'rgba(255, 186, 19, 0.4)');
      this.gradient3.addColorStop(0.5, 'rgba(255, 186, 19, 0.12)');
      this.gradient3.addColorStop(1, 'rgba(255, 186, 19, 0)');

      this.gradient4.addColorStop(0, 'rgba(249, 88, 90, 0.4)');
      this.gradient4.addColorStop(0.5, 'rgba(249, 88, 90, 0.12)');
      this.gradient4.addColorStop(1, 'rgba(249, 88, 90, 0)');
      this.gradient = [
        this.gradient0,
        this.gradient1,
        this.gradient2,
        this.gradient3,
        this.gradient4,
      ];
      this.colors = ['#00a86b', '#41b3e9', '#7a7a7a', '#ffba13', '#f9585a'];
      this.smiles.forEach((smile, index) => {
        this.array.push({
          label: smile,
          borderColor: this.colors[index],
          pointBackgroundColor: 'white',
          borderWidth: 1.5,
          pointBorderColor: 'grey',
          backgroundColor: this.gradient[index],
          data: this.values[index],
        });
      });
      // prettier-ignore
      this.renderChart(
        {
          labels: this.hours,
          datasets: this.array,
        },
        { responsive: true, maintainAspectRatio: false },
      );
    },
  },
  computed: {},
  mounted() {
    this.createGraf();
  },
};
</script>

<style lang="scss" scoped>
.areaChart {
  min-width: 320px;
  border-radius: 4px;
  padding: 20px 5px 20px 5px;
  background-color: var(--stat-background);
}
</style>
