<template>
  <div>
    <div v-if="this.dataLoaded == false"></div>
    <div v-else class="wrapper">
      <h1 id="title">Workout Dashboard</h1>
      <div id="weight-chart">
        <weight-chart :weightsData="this.weightsData" :datesData="this.datesData"/>
      </div>
      <div id="prs">
        <!-- <h6 style="text-align:center;margin-top:40px;">PRs</h6> -->
      </div>
      <div id="calendar">
        <Calendar :dailyData="this.sheetsData" :monthYearsData="this.monthYearsData"/>
      </div>
    </div>
  </div>

</template>

<script>
import WeightChart from '@/components/WeightChart';
import Calendar from '@/components/Calendar';
import { GoogleSpreadsheet } from 'google-spreadsheet';

export default {
  name: 'App',
  components: {
    Calendar,
    WeightChart
  },
  data: () => ({
      dataLoaded: false,
      sheetsData: "teehee",
      weightsData: [180, 175, 175, 178],
      datesData: ['10/20', '10/28', '11/4', '11/11'],
      monthYearsData: "November"
  }),
  created () {
    const doc = new GoogleSpreadsheet('1BMrVDwdhs8VhEeQGWc4AAbSehpF09hGupQgriCcJjn4')
    
    async function test() {
      doc.useApiKey(process.env.VUE_APP_NOT_SECRET_CODE);
      await doc.loadInfo()
      const sheet = doc.sheetsByIndex[0];
      const rows = await sheet.getRows();
      var fullData = {};
      let monthYears = new Set();
      var dates = [];
      var weights = [];

      var i;
      for (i = 0; i < rows.length; i++) {
          var year = rows[i].year;
          var monthName = rows[i].monthName;
          // var monthNumber = rows[i].monthNumber;
          var day = rows[i].day;
          // var weight = rows[i].weight;
          weights.push(rows[i].weight);
          var date = rows[i].date;
          dates.push(rows[i].date);
          var didLift = rows[i].didLift;
          var didCardio = rows[i].didCardio;
          var cardioDescription = rows[i].cardioDescription;
          var liftDescription = rows[i].liftDescription;
          var monthYear = monthName + " " + year;
          if (!(monthYear in fullData)) {
            fullData[monthYear] = {}
            monthYears.add(monthYear);
          }
          if (!(day in fullData[monthYear])) {
            fullData[monthYear][day] = {date: date,
                                // weight: weight,
                                didLift: didLift,
                                didCardio: didCardio,
                                cardioDescription: cardioDescription,
                                liftDescription: liftDescription};
            
          } 
      }
      monthYears = [...monthYears];
      return [fullData, weights, dates, monthYears]
    }
    test().then((res) => this.setData(res));
  },
  methods: {
        setData(res) {
          var fullData = res[0];
          var weights = res[1]; 
          var dates = res[2];
          var monthYears = res[3];
          this.sheetsData = fullData;
          this.weightsData = weights;
          this.datesData = dates;
          this.monthYearsData = monthYears;
          this.dataLoaded = true;
        }
  }
}

</script>


<style>
.wrapper {
  display: grid;
  grid-template-areas: "title"
                       "weight-chart"
                       "prs"
                       "calendar";
  grid-template-columns: 100%;
  grid-template-rows: 10vh 20vh 20vh auto;
}

.wrapper > #title {
  grid-area: title;
  text-align: center;
  margin: 0px;
  font-family: 'Black Han Sans', sans-serif;
}

.wrapper > #weight-chart {
  grid-area: weight-chart;
}

.wrapper > #calendar {
  grid-area: calendar;
}

.wrapper > #prs {
  grid-area: prs;
}
</style>

