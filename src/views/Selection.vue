<template>
  <div class="home">
    <h2 class="text-independence text-lg mb-5">Terminauswahl</h2>

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
