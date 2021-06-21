<template>
  <div class="Calendar">
    <div class="KW">KW</div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Calendar",
  props: {
    username: {
      type: String,
      required: false,
    },
  },
  data: function () {
    return {
      count: 0,
    };
  },
  mounted: function () {
    axios.get("/data/data.json").then((response) => {
      console.log(response.data);
    });
  },
};
</script>


