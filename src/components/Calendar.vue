<template>
  <div id="calendar-container">
    <h1>Calendar</h1>
    <div id="calendar">
      <h1>
        <a @click="lastMonth">&lt;</a>
        {{ year }} 년
        {{month}} 월
        <a @click="nextMonth">></a>
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
          <span v-if="(i+1)-firstDay === today && i%7 ===0 " style="
            color:red;
             background-color:#bbb;
            border: none 1px;
            border-radius: 50%;
          ">
            {{ date.num }}
          </span>

          <span v-else-if="(i+1)-firstDay === today && i%7 ===6 " style="
            color:blue;
            background-color:#bbb;
            border: none 1px;
            border-radius: 50%;
          ">
            {{ date.num }}
          </span>

          <span v-else-if="(i+1)-firstDay === today" style="
            background-color:#bbb;
            border: none 1px;
            border-radius: 50%;
          ">
            {{ date.num }}
          </span>
          <span v-else-if="i%7===0" style="color:red">
            {{ date.num }}
          </span>
          <span v-else-if="i%7===6" style="color:blue">
            {{ date.num }}
          </span>
          <span v-else>
            {{ date.num }}
          </span>
          <p 
            v-for="memo, i in date.memos" :key="i"
            style="margin:2px; background-color: aquamarine; text-align: left;"
          >
            {{ memo.id }}
          </p>
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
      today: 0,
    }
  },
  created() {
    this.setDate();
    this.calcDate();
    this.dateSetup();
  },
  methods: {
    dateSetup() {
      for(let i=0; i<42; i++) {
        if(i < this.firstDay || i > this.lastDay + this.firstDay - 1) {
          this.dates.push({
            id:`${i}`,
            num: ' ',
            memos: '',
            });
        }
        // memo 확인 용 더미데이터
        else if(i === 8){
          this.dates.push({
           id:`${i}`,
           num: (i+1)-this.firstDay,
           memos: [
            {id: '첫번째 할일'},
            {id: '두번째 할일'},
          ]
          })
        }
        else {
          this.dates.push({
           id:`${i}`,
           num: (i+1)-this.firstDay,
           memos: ''
          })
        };
      };
    },
    setDate() {
      const getDate = new Date();
      this.month = getDate.getMonth() + 1 > 9 ? getDate.getMonth() + 1 : '0' + (getDate.getMonth() + 1);
      this.year = getDate.getFullYear();
      this.today = getDate.getDate();
     
    },
    calcDate() {
      const timeDate = this.year+'-'+this.month+'-01';
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
        this.month--;
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
      else if(this.month >= 9) {
        this.month++;
      }
      else {
        this.month = '0'+(parseInt(this.month) + 1);
      }
      this.calcDate();
      this.dates = [];
      this.dateSetup();
    },
  },
}
</script>

<style>
  #calendar-container {
    margin: 0;
    text-align: center;
  }

  #days {
    display:grid;
    grid-template-columns: repeat(7, 1fr);
    grid-template-rows: 40px;
    grid-gap: 0.1px;
  }
  #days > div {
    border: 1px solid #bbb;
  }
  
  #dates {
    display:grid;
    grid-template-columns: repeat(7, 1fr);
    grid-auto-rows: minmax(80px, auto);
    grid-gap: 0.1px;
  }
  #dates > div {
    border: 1px solid #bbb;
  }

  main {
    text-align: center;
  }

  a {
    cursor: pointer;
    color: #999;
  }
</style>