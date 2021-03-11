<template>
  <v-container class="app-top-bar">
    <h2 class="text-h5 text-center mb-3 mt-5">
      Classificação
    </h2>
    <v-simple-table>
      <template v-slot:default>
        <thead>
          <tr>
            <th>
              Posição
            </th>
            <th class="text-center">
              Clubes
            </th>
            <th class="text-right">
              Pontos
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(clube, index) of clubesListaOrdenada" :key="clube.id">
            <td>{{ index + 1 }}</td>
            <td>
              <v-avatar size="24">
                <img :src="clube.escudo" :alt="clube.nome" />
              </v-avatar>
              <router-link to="/corinthians">
                <span class="pl-2">{{ clube.nome }} </span>
              </router-link>
            </td>
            <td class="text-center">{{ clube.pontos }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </v-container>
</template>

<script>
export default {
  name: "ClubesLista",
  data() {
    return {
      clubesLista: [],
    };
  },
  computed: {
    clubesListaOrdenada() {
      const listaOrdenada = this.clubesLista
        .slice(0)
        .sort((a, b) => (a.pontos > b.pontos ? -1 : 1));
      return listaOrdenada;
    },
  },
  created() {
    fetch("https://hackthon-decola.firebaseio.com/clubes-lista.json")
      .then((resposta) => resposta.json())
      .then((json) => {
        this.clubesLista = json;
        console.log(this.clubesLista);
      });
  },
};
</script>

<style scoped>
.app-top-bar a {
  text-decoration: none;
  color: #fff;
}
</style>
