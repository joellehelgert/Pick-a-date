<template>
  <div v-if="showCalendar">
    <Calendar :username="username" />
  </div>
  <div v-else>
    <input
      v-model="username"
      placeholder="dein Name"
      type="text"
      class="w-4/6 text-lg border p-3 b-r-0"
    />
    <button
      class="
        p-3
        text-lg
        rounded-r
        bg-yellow-100 bg-greenSheen
        border border-greenSheen
        text-white
      "
      @click="showSelection"
    >
      Zur Terminauswahl
    </button>
  </div>
</template>

<script>
import Calendar from "./Calendar.vue";

export default {
  name: "Input",
  props: {},
  components: { Calendar },
  data: function () {
    return { username: null, showCalendar: false };
  },
  methods: {
    showSelection: function () {
      if (this.username) {
        this.showCalendar = true;
      }
    },
  },
};
</script>

