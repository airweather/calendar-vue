<template>
  <div id="calendar-container">
    <h1>Calendar</h1>
    <div id="calendar">
      <h1>
        <button>before</button>
        {{ year }} 년
        {{month}} 월
        <button>next</button>
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
      firstDay: 1,
      lastDay: 0,
      month: 0,
      year: 0,
    }
  },

  created() {
    this.setDate();
    this.dateSetup();
    // this.datePut();
  },
  
  methods: {
    dateSetup() {
      for(let i=0; i<42; i++) {
        this.dates.push({
         id:`${i}`
        })
      }
      for(let i=0; i<42; i++) {
        if(i<this.firstDay || i>this.lastDay) {
          this.dates[i].num = ' ';
        }
        else {
          this.dates[i].num = (i+1)-this.firstDay;
        }
      }
      // console.log('setup : ', this.dates)
    },
    setDate() {

      const date = new dayjs();
      this.month = (date.month())+1;
      this.year = date.year();
      this.lastDay = date.daysInMonth();
      this.firstDay = date.startOf('month').$W;
    }
    
    // datePut() {
    //   for(let i=0; i<this.lastDay; i++) {
    //     this.dates[i].num = i;
    //   }
    //   console.log('put : ',this.dates)
    // }
  }
}
</script>

<style>
  #calendar-container {
    margin: 0;
    text-align: center;
    height: 100%;
  }
  
  #days {
    display:grid;
    grid-template-columns: repeat(7, 1fr);
    height: 40px;
  }
  
  #dates {
    display:grid;
    grid-template-columns: repeat(7, 1fr);
    height: 40px;
  }

  main {
    text-align: center;
  }
</style>