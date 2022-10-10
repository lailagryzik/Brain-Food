<template>
  <v-row>
    <v-col class="text-center">
      {{ name }}
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: "InspirePage",
  data: () => ({
    name: "",
    versicherungsnummer: "",
  }),
  mounted() {
    this.name = localStorage.getItem("name");
    this.versicherungsnummer = localStorage.getItem("versicherungsnummer");
  },
};
</script>
