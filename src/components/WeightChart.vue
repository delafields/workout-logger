<template>
  <canvas ref="myChart" width="500" height="100"></canvas>
</template>


<script>
import Chart from 'chart.js';

export default {
  name: 'WeightChart',
  props: ["weightsData", "datesData"],
  mounted() {
    new Chart(this.$refs.myChart, {
      type: 'line',
      data: {
        labels: this.datesData,
        datasets: [
          {
            label: 'Weight',
            data: this.weightsData,
            borderColor: "rgb(15,32,39)",
            fill: false,
            pointBackgroundColor: '#42CC8C',
            borderWidth: 1,
            pointBorderColor: 'white',
          }
        ]
      },
      options: {
        // title: {
        //     display: true,
        //     text: 'WEIGHT',
        //     fontColor: '#0F2027',
        //     fontSize: 14
        // },
        scales: {
          yAxes: [{
            // scaleLabel: {
            //   display: true,
            //   labelString: 'Weight',
            //   fontColor: '#0F2027'
            // },
            ticks: {
              suggestedMin: 160,
              suggestedMax: 195,
              stepSize: 15
            },
            gridLines: {
              display: true
            }
          }],
          xAxes: [{
              ticks: {
                autoSkip: true,
                maxTicksLimit: 20
                },
              gridLines: {
                display: false
              }
          }]
          },
          legend: {
            display: false
          }
    }
    });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
