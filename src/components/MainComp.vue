<template>
  <div>
    <div><input @keyup="getInfo()" v-model="nomeFilm" type="text" /></div>
    <div
      class="card"
      v-for="(element, index) in dataFilms"
      :key="index"
      :singleItem="element"
    >
      <div>{{ element.title }}</div>
      <div>{{ element.original_title }}</div>
      <div v-if="element.original_language == 'en'"><img class="flag" src="../assets/img/Flag_of_the_United_Kingdom.svg" alt="flag of the UK"></div>
      <div v-else-if="element.original_language == 'it'"><img class="flag" src="../assets/img/Flag_of_Italy.svg" alt="flag of Italy"></div>
      <div v-else><img class="flag" src="../assets/img/PACE_flag_(without_text).svg" alt="Peace Flag"></div>
      <div>{{element.vote_average}}</div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      dataFilms: [],
    };
  },
  mounted() {},
  methods: {
    getInfo() {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=e99307154c6dfb0b4750f6603256716d&query=${this.nomeFilm}`
        )
        .then((response) => {
          this.dataFilms = response.data.results;
        });
    },
  },
};
</script>

<style scoped lang="scss">
.flag{
    width: 30px;
}
</style>