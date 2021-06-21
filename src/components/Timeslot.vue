<template>
  <li
    class="timeslot p-5 m-3 rounded bg-deepChampagne"
    v-on:click="selectTimeslot"
  >
    {{ timeslot.time }}
    <p v-if="timeslot.name">{{ timeslot.name }}</p>
    <p v-else>freier Termin</p>
    <span v-if="selected"> check </span>
  </li>
</template>

<script>
export default {
  name: "Calendar",
  props: ["timeslot", "kw", "date", "time"],
  data: () => {
    return { selected: false };
  },
  methods: {
    selectTimeslot: function (e) {
      console.log("click", e);
      this.selected = !this.selected;
      this.$emit("updateValue", {
        date: this.date,
        time: this.time,
        kw: this.kw,
      });
    },
  },
};
</script>


