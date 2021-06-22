<template>
  <li
    class="timeslot p-5 m-3 rounded border-2 border-transparent"
    :class="{
      'border-greenSheen bg-greenSheen text-white': timeslot.selected,
      'border-terraCotta': timeslot.error,
      'bg-deepChampagne': !timeslot.selected,
    }"
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
    selectTimeslot: function () {
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


