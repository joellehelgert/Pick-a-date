<template>
  <div class="overview">
    <h2 class="text-greenSheen text-xl">Terminübersicht</h2>
    <Calendar :interactable="false"> </Calendar>
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

