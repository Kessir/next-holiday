<template>
  <div id="app">
    <header>
      <h2>Next Holiday</h2>
    </header>
    <div class="main">
      <div>in {{timeToHoliday}} Days </div>
      <h2> {{nextHoliday.name}} </h2>
      <h4> {{ nextHoliday.formattedDate }} </h4>
    </div>
   
  </div>
</template>

<script>
import holidays from "./assets/data/gh-holidays";
import moment from "moment";

// const DATE_TIME_FORMAT = "MMMM Do YYYY, h:mm a";
const DATE_FORMAT = "MMMM Do YYYY";

export default {
  name: "app",
  created() {
    this.updateDate();
  },
  data() {
    return {
      holidays: holidays,
      today: new Date(),

    };
  },
  computed: {
    nextHoliday() {
      for (const holiday of this.holidays) {
        if (moment(holiday.date, "DD-MM-YYYY").isAfter(this.today)) {
          const nextHoliday = {...holiday, formattedDate: moment(holiday.date, "DD-MM-YYYY").format(DATE_FORMAT) }
          return nextHoliday;
        }
      }
    },
    remainingHolidaysArray() {
      return this.holidays;
    },
    timeToHoliday() {
      return moment(this.nextHoliday.date, "DD-MM-YYYY").diff(
        this.today,
        "days"
      );
    }
  },
  methods: {
    updateDate() {
      this.today = new Date();
      setInterval(() => {
        this.today = new Date();
      }, 30000);
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  /* color: #2c3e50; */
  margin-top: 30px;
}
.main {
  /* margin-top: 30px; */
}
h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
