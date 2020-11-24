<template>
  <v-data-table
    :headers="headers"
    :items="desserts"
    :items-per-page="5"
    class="elevation-1"
  ></v-data-table>
</template>

<script>
export default {
  data() {
    return {
      headers: [
        { text: "ID", value: "id" },
        { text: "Descrição", value: "descricao" },
        { text: "created_at", value: "created_at" },
      ],
      desserts: [],
    };
  },
  created(){
      this.listarPerfils()
  },
  methods: {
    listarPerfils() {
      const me = this;
      let rota = "/perfils";

      this.axios
        .get(rota, this.configuration)
        .then(function(response) {
          me.desserts = response.data;
        })
        .catch(function(error) {
          // eslint-disable-line no-unused-vars
        });
    },
  },
};
</script>
