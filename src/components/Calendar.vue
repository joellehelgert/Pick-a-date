<template>
  <div v-if="error">
    Sorry! Ein Fehler ist aufgetreten, bitte lade die Seite nochmal neu!
  </div>
  <div v-if="loading">einen Moment, der Kalendar wird geladen</div>
  <div v-if="!loading" class="Calendar">
    <div class="flex justify-between w-full">
      <p
        class="mt-3 text-lg"
        :class="{ 'text-greenSheen': totalSelected == 3 }"
      >
        Es wurden {{ this.totalSelected }} von 3 Terminen ausgewählt
      </p>
      <button
        class="p-3 rounded text-lg border border-terraCotta"
        :class="{
          'bg-greenSheen border-greenSheen text-white cursor-pointer':
            totalSelected == 3,
          'cursor-not-allowed': totalSelected < 3,
        }"
        @click="selectTimeslots"
      >
        Termine auswählen
      </button>
    </div>

    <div class="KW flex flex-wrap" v-for="date in dates" :key="date.KW">
      <h2
        class="
          w-full
          text-greenSheen text-xl
          border-2 border-greenSheen
          rounded
          mb-3
          mt-6
          p-4
        "
      >
        KW {{ date.KW }}
      </h2>

      <ul
        class="day w-full lg:w-1/6 flex flex-col p-2"
        v-for="days in date.days"
        :key="days.day"
      >
        <span class="text-lg text-white bg-terraCotta rounded p-1">
          {{ days.day }},
          {{ days.date }}
        </span>
        <template v-if="!loading && !days.timeslots">
          <p class="mt-6">keine Termine für diesen Tag</p>
        </template>
        <div class="h-full flex flex-col justify-end">
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
        </div>
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
      totalSelected: 0,
    };
  },
  mounted: function () {
    this.loading = true;
    this.error = null;
    axios
      .get(
        "https://pick-a-date-44000-default-rtdb.europe-west1.firebasedatabase.app/calendar.json"
      )
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
      if (this.totalSelected == 3) {
        console.log("selecting all", e);
        axios
          .put(
            "https://pick-a-date-44000-default-rtdb.europe-west1.firebasedatabase.app/calendar.json",
            this.dates
          )
          .then((response) => {
            console.log(response);
          })
          .catch((error) => {
            console.error(error);
            this.error = error;
          });
      }
    },
    applyRules: function (current, arr, index, value) {
      const check = [-2, -1, 1, 2];
      check.forEach((operator) => {
        let elem = arr[index + operator];
        if (elem) {
          if (
            elem.start - current.start < -149 ||
            elem.start - current.start < 150
          ) {
            // not disabled
            arr[index + operator].disabled = value;
          } else {
            // disabled
            arr[index + operator].disabled = !value;
          }
        }
      });

      return arr;
    },
    updateValue: function (updatable) {
      this.dates.forEach((elem) => {
        if (elem.KW == updatable.kw) {
          elem.days.forEach((day) => {
            if (day.date == updatable.date) {
              day.timeslots.forEach((timeslot, index) => {
                if (timeslot.time == updatable.time) {
                  if (timeslot.name == this.username) {
                    timeslot.name = "";
                    timeslot.selected = false;
                    this.totalSelected--;

                    day.timeslots = this.applyRules(
                      timeslot,
                      day.timeslots,
                      index,
                      false
                    );
                  } else if (timeslot.name != "") {
                    timeslot.error = "Already taken";
                    timeslot.selected = false;
                  } else {
                    timeslot.selected = true;
                    timeslot.name = this.username;
                    this.totalSelected++;
                    day.timeslots = this.applyRules(
                      timeslot,
                      day.timeslots,
                      index,
                      true
                    );
                  }
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


