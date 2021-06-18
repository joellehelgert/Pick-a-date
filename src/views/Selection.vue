<template>
  <div class="home">
    <h1 class="text-red-500">Terminauswahl</h1>

    <Input />
  </div>
</template>

<script>
// @ is an alias to /src
import Input from "@/components/Input.vue";

export default {
  name: "Home",
  components: {
    Input,
  },
};
</script>
