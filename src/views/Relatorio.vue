<template>
  <v-container>
    <v-data-table
      :search="search"
      :headers="headers"
      :items="atividades"
      class="elevation-1"
    >
      <template v-slot:top>
        <v-toolbar flat>
          <v-toolbar-title>Atividades</v-toolbar-title>

          <v-spacer></v-spacer>

          <v-text-field
            class="text-xs-center"
            v-model="search"
            label="Pesquisa"
            single-line
            hide-details
          ></v-text-field>

          <v-spacer></v-spacer>
          <a-button type="primary" @click="showModal">
            Adicionar Atividade <a-icon type="plus" />
          </a-button>
        </v-toolbar>
      </template>

      <template v-slot:[`item.action`]="{ item }">
        <a-tooltip placement="left">
          <template slot="title">
            <span>Excluir</span>
          </template>

          <v-icon
            big
            class="mr-2"
            @click="excluir(item)"
            style="color: #F24607;"
          >
            mdi-close-thick
          </v-icon>
        </a-tooltip>

        <a-tooltip placement="left">
          <template slot="title">
            <span>Editar</span>
          </template>

          <v-icon big class="mr-2" @click="editar(item)">
            mdi-table-edit
          </v-icon>
        </a-tooltip>
      </template>

      <template v-slot:[`item.link`]="{ item }">
        <a-tooltip placement="top">
          <template slot="title">
            <span>Adicionar Anexo</span>
          </template>

          <a-button size="small" @click="showUpload(item)">
            <a-icon type="plus" />
          </a-button>
        </a-tooltip>
      </template>
    </v-data-table>
  </v-container>
</template>
<script>
export default {
  data() {
    return {
      headers: {
        Token: this.$store.state.portarias_token,
      },
      search: "",
      atividades: [],
      headers: [
        { text: "Ações", value: "action" },
        { text: "Descrição", value: "descricao" },
        { text: "Status", value: "status" },
        { text: "Professor", value: "user.name" },
        { text: "Link", value: "link" },
      ],
    };
  },
  created() {
    this.listarAtividades();
  },
  methods: {
    listarAtividades() {
      let rota = "/atividades";

      this.axios.get(rota).then((res) => {
        this.atividades = res.data;
      });
    },
  },
};
</script>
