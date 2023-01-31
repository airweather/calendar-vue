<template>
  <div id="calendar-container">
    <h1>Calendar</h1>
    <div id="calendar">
      <h1>
        <button @click="lastMonth">before</button>
        {{ year }} 년
        {{month}} 월
        <button @click="nextMonth">next</button>
      </h1>
      <div id="days">
        <div v-for="day, i in days" :key="i">
          <span v-if="i===0" style="color:red">
            {{ day }}
          </span>
          <span v-else-if="i===6" style="color:blue">
            {{ day }}
          </span>
          <span v-else>
            {{ day }}
          </span>
        </div>
      </div>
      <div id="dates">
        <div v-for="date, i in dates" :key="date.id">
          <span v-if="i%7===0" style="color:red">
            {{ date.num }}
          </span>
          <span v-else-if="i%7===6" style="color:blue">
            {{ date.num }}
          </span>
          <span v-else>
            {{ date.num }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import dayjs from "dayjs";

export default {
  data() {
    return {
      days:['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
      dates:[],
      firstDay: 0,
      lastDay: 0,
      month: 0,
      year: 0,
    }
  },

  created() {
    this.setDate();
    this.calcDate();
    this.dateSetup();
    // this.datePut();
  },
  
  methods: {
    dateSetup() {
      for(let i=0; i<42; i++) {
        if(i < this.firstDay || i > this.lastDay + this.firstDay - 1) {
          this.dates.push({
            id:`${i}`,
            num: ' ',
            })
        }
        else {
          this.dates.push({
           id:`${i}`,
           num: (i+1)-this.firstDay,
          })
        }
      }
    },
    setDate() {
      const getDate = new Date();
      this.month = getDate.getMonth() + 1 > 9 ? getDate.getMonth() + 1 : '0' + (getDate.getMonth() + 1);
      this.year = getDate.getFullYear();
    },
    calcDate() {
      console.log(this.year, this.month);
      const timeDate = this.year+'-'+this.month+'-01'
      const date = new dayjs(timeDate);
      this.lastDay = date.daysInMonth();
      this.firstDay = date.startOf('month').$W;
    },

    lastMonth() {
      if(this.month <= 1) {
        this.month = 12;
        this.year--;
      }
      else if(this.month > 10) {
        this.month--
      }
      else {
        this.month = '0'+(this.month - 1);
      }
      this.calcDate();
      this.dates = [];
      this.dateSetup();
    },
    nextMonth() {
      if(this.month >= 12) {
        this.month = 1;
        this.year++;
      }
      else if(this.month > 9) {
        this.month++
      }
      else {
        this.month = parseInt(this.month) + 1
      }
      this.calcDate();
      this.dates = [];
      this.dateSetup();
    },
  },
}
</script>

<style>
  /* #calendar {
    height:1000px
  } */

  #calendar-container {
    margin: 0;
    text-align: center;
  }
  
  #days {
    height: 30px;
    display:grid;
    grid-template-columns: repeat(7, 1fr);
  }
  
  #dates {
    height: 100px;
    display:grid;
    grid-template-columns: repeat(7, 1fr);
  }

  main {
    text-align: center;
  }
</style>