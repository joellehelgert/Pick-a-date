<template>
  <li
    class="timeslot p-2 m-2 rounded border-2 border-transparent"
    :class="setStatus()"
    v-on:click="selectTimeslot"
  >
    {{ timeslot.time }}
    <p v-if="timeslot.name">{{ timeslot.name }}</p>
    <p v-else>freier Termin</p>
  </li>
</template>

<script>
export default {
  name: "Calendar",
  props: ["timeslot", "kw", "date", "time"],
  methods: {
    setStatus: function () {
      if (this.timeslot.selected) {
        return "border-greenSheen bg-greenSheen text-white cursor-pointer";
      } else if (this.timeslot.error) {
        return "border-terraCotta cursor-not-allowed";
      } else if (this.timeslot.disabled) {
        return "bg-transparent border-terraCotta cursor-not-allowed";
      } else {
        return " bg-deepChampagne cursor-pointer";
      }
    },
    selectTimeslot: function () {
      if (!this.timeslot.disabled) {
        this.selected = !this.selected;
        this.$emit("updateValue", {
          date: this.date,
          time: this.time,
          kw: this.kw,
        });
      }
    },
  },
};
</script>


