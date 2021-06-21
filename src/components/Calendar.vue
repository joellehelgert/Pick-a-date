<template>
  <div v-if="error">Sorry! An error has occured. Please Reload the page</div>
  <div v-if="loading">
    We are loading the monsters please wait for a moment. Sometimes they are a
    little shy!
  </div>
  <div v-if="!loading" class="Calendar">
    <button
      class="
        p-3
        bg-yellow-100 bg-greenSheen
        border border-greenSheen
        text-white
      "
      @click="selectTimeslots"
    >
      Termine auswählen
    </button>
    <div class="KW" v-for="date in dates" :key="date.KW">
      <h2>KW {{ date.KW }}</h2>

      <ul
        class="day w-1/5 flex flex-col p-2 rounded border-2 border-greenSheen"
        v-for="days in date.days"
        :key="days.day"
      >
        {{
          days.day
        }},
        {{
          days.date
        }}
        <Timeslot
          v-for="timeslot in days.timeslots"
          :key="days.day + timeslot.time"
          :kw="date.KW"
          :date="days.date"
          :time="timeslot.time"
          :username="username"
          :timeslot="timeslot"
          @update-value="updateValue"
        >
        </Timeslot>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Timeslot from "./Timeslot.vue";

export default {
  name: "Calendar",
  components: { Timeslot },
  props: {
    username: {
      type: String,
      required: false,
    },
  },
  data: function () {
    return {
      loading: false,
      error: null,
      dates: [],
    };
  },
  mounted: function () {
    this.loading = true;
    this.error = null;
    axios
      .get("/data/data.json")
      .then((response) => {
        console.log(response.data);
        this.dates = response.data;
        this.loading = false;
      })
      .catch((error) => {
        console.error(error);
        this.error = error;
      });
  },
  methods: {
    selectTimeslots: function (e) {
      console.log("selecting all", e);
      axios({
        method: "post",
        url: "/data/data.json",
        data: this.dates,
      });
      // axios
      //   .post("/data/data.json", this.dates)
      //   .then((response) => {
      //     console.log(response);
      //   })
      //   .catch((error) => {
      //     console.error(error);
      //     this.error = error;
      //   });
    },
    updateValue: function (updatable) {
      this.dates.forEach((elem) => {
        if (elem.KW == updatable.kw) {
          elem.days.forEach((day) => {
            if (day.date == updatable.date) {
              day.timeslots.forEach((timeslot) => {
                if (timeslot.time == updatable.time) {
                  timeslot.name = this.username;
                }
              });
            }
          });
        }
      });
    },
  },
};
</script>


