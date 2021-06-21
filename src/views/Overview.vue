<template>
  <div class="overview">
    <h1>Terminübersicht</h1>
    <Calendar username="Joelle"> </Calendar>
  </div>
</template>

<script>
// @ is an alias to /src
import Calendar from "@/components/Calendar.vue";

export default {
  name: "Overview",
  components: {
    Calendar,
  },
};
</script>

