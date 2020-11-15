<template>
  <div id="calendar-wrapper">

    <DayModal v-if="modalVisible" 
         @close="modalVisible = false" 
         :name="modalDate"
         :data="modalData"
         id="modal"/>

    <div v-for="(dayData, monthYear) in dailyData" :key="monthYear">

      <h2 class="monthYear">{{monthYear}}</h2>

      <div id="days">
        <button class="day"
                v-for="(data, day) of dayData" 
                :key="monthYear + day"
                type="button" 
                @click="openModal(data.date, data)">
          <div v-if="data.didCardio == 'FALSE' && data.didLift == 'FALSE'" class="no-activity">
            {{day}}
          </div>
          <div v-else class="activity">
            {{day}} 
            <Badge v-if="data.didCardio == 'TRUE'" badgeType="🏃‍♂️"/>
            <Badge v-if="data.didLift == 'TRUE'" badgeType="💪"/>
          </div>
          </button>
        </div>

    </div>
    
  </div>
</template>

<script>
import DayModal from '@/components/DayModal.vue'
import Badge from '@/components/Badge.vue'

export default {
  name: 'Calendar',
  props: ["dailyData", "monthYearsData"],
  data: () => ({
      modalVisible: false,
      modalDate: null,
      modalData: null
  }), 
  methods: {
    openModal(date, data) {
      this.modalDate = date
      this.modalData = data
      this.modalVisible = true
    }
  },
  components: {
    DayModal, Badge
  }
}
</script>

<style>
#calendar-wrapper {
  margin-top: 40px;
  margin-left: 5%;
  margin-right: 5%;
}

/* Mobile */
/* only screen and (min-width: 480px) */

/* Tablet */
@media (max-width: 499px) {
  #days {
      display: grid;
      /* grid-gap: 5px; */
      grid-column-gap: 10px;
      grid-row-gap: 10px;
      width: 100%;
      grid-template-columns: repeat(4, 1fr);
  }
}

@media (min-width: 500px) {
  #days {
      display: grid;
      /* grid-gap: 5px; */
      grid-column-gap: 10px;
      grid-row-gap: 10px;
      width: 100%;
      grid-template-columns: repeat(7, 1fr);
  }
}

.day{
    border: 3px solid #000074;
    border-radius: 4px;
    width: 100%;
    height: 40px;
    background-color:#42CC8C;
    cursor: pointer;
}

.activity {
    color: white;
    font-size: 20px;
    font-family: 'Black Han Sans', sans-serif;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
}

.no-activity {
    color: white;
    font-size: 20px;
    text-align: left;
    font-family: 'Black Han Sans', sans-serif;
    padding-left: 11px;
}

.monthYear{
  font-family: 'Black Han Sans', sans-serif;
}

#modal {
    position: fixed;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    border-radius: 4px;
    width: 60%;
    margin-left: auto;
    margin-right: auto;
    background-color: #0F2027;  /* fallback for old browsers */   
    box-shadow: 0 10px 20px rgba(0,0,0,0.19), 0 6px 6px rgba(0,0,0,0.23);
}
</style>