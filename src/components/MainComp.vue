<template>
  <div>
    <div>
      <input
        @keyup="getInfoFilms(), concatArrays(), getInfoTv()"
        v-model="nomeFilm"
        type="text"
      />
    </div>
    <section class="d-flex flex-wrap">
      <div
        class="card"
        v-for="(element, index) in dataAll"
        :key="index"
        :singleItem="element"
      >
        <div class="front-card">
          <img
            :src="`https://image.tmdb.org/t/p/w342/${element.poster_path}`"
            alt=""
          />
        </div>
        <div class="back-card" >
          <div>{{ element.title }}</div>
          <div>{{ element.name }}</div>
          <div>{{ element.original_title }}</div>
          <div v-if="element.original_language == 'en'">
            <img
              class="flag"
              src="../assets/img/Flag_of_the_United_Kingdom.svg"
              alt="flag of the UK"
            />
          </div>
          <div v-else-if="element.original_language == 'it'">
            <img
              class="flag"
              src="../assets/img/Flag_of_Italy.svg"
              alt="flag of Italy"
            />
          </div>
          <div v-else>
            <img
              class="flag"
              src="../assets/img/PACE_flag_(without_text).svg"
              alt="Peace Flag"
            />
          </div>

          <div v-if="parseInt(element.vote_average / 2) == 5">
            <img src="../assets/img/star-fill.svg" alt="" />
            <img src="../assets/img/star-fill.svg" alt="" />
            <img src="../assets/img/star-fill.svg" alt="" />
            <img src="../assets/img/star-fill.svg" alt="" />
            <img src="../assets/img/star-fill.svg" alt="" />
          </div>
          <div v-else-if="parseInt(element.vote_average / 2) == 4">
            <img src="../assets/img/star-fill.svg" alt="" />
            <img src="../assets/img/star-fill.svg" alt="" />
            <img src="../assets/img/star-fill.svg" alt="" />
            <img src="../assets/img/star-fill.svg" alt="" />
            <img src="../assets/img/star.svg" alt="" />
          </div>
          <div v-else-if="parseInt(element.vote_average / 2) == 3">
            <img src="../assets/img/star-fill.svg" alt="" />
            <img src="../assets/img/star-fill.svg" alt="" />
            <img src="../assets/img/star-fill.svg" alt="" />
            <img src="../assets/img/star.svg" alt="" />
            <img src="../assets/img/star.svg" alt="" />
          </div>
          <div v-else-if="parseInt(element.vote_average / 2) == 2">
            <img src="../assets/img/star-fill.svg" alt="" />
            <img src="../assets/img/star-fill.svg" alt="" />
            <img src="../assets/img/star.svg" alt="" />
            <img src="../assets/img/star.svg" alt="" />
            <img src="../assets/img/star.svg" alt="" />
          </div>
          <div v-else-if="parseInt(element.vote_average / 2) == 1">
            <img src="../assets/img/star-fill.svg" alt="" />
            <img src="../assets/img/star.svg" alt="" />
            <img src="../assets/img/star.svg" alt="" />
            <img src="../assets/img/star.svg" alt="" />
            <img src="../assets/img/star.svg" alt="" />
          </div>
          <div v-else-if="parseInt(element.vote_average / 2) == 0">
            <img src="../assets/img/star.svg" alt="" />
            <img src="../assets/img/star.svg" alt="" />
            <img src="../assets/img/star.svg" alt="" />
            <img src="../assets/img/star.svg" alt="" />
            <img src="../assets/img/star.svg" alt="" />
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

        
<script>
import axios from "axios";
export default {
  data() {
    return {
      dataFilms: [],
      dataTv: [],
      dataAll: [],
      nomeFilm: "",
    };
  },
  mounted() {},
  methods: {
    getInfoFilms() {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=e99307154c6dfb0b4750f6603256716d&query=${this.nomeFilm}`
        )
        .then((response) => {
          this.dataFilms = response.data.results;
        });
    },
    getInfoTv() {
      axios
        .get(
          `https://api.themoviedb.org/3/search/tv?api_key=e99307154c6dfb0b4750f6603256716d&query=${this.nomeFilm}`
        )
        .then((response) => {
          this.dataTv = response.data.results;
        });
    },
    concatArrays() {
      this.dataAll = this.dataFilms.concat(this.dataTv);
    },
  },
};
</script>

<style scoped lang="scss">
.flag {
  width: 30px;
}
.card {
  position: relative;
  
  transition: transform 1000ms;
  transform-style: preserve-3d;
  width: calc((100vw/4) - 10px);
}
.card:hover {
  transform: rotateY(180deg);
}
.card > .front-card > img {
  box-sizing: border-box;
  display: block;
  width: 100%;
}
.front-card {
  height: 100%;
}
.card:hover img {
  display: none;
}
.card:hover .front-card {
  display: none;
}
.back-card {
  transform: rotateY(180deg);
  width: calc((100vw/4) - 10px);
  height: 100%;
}
.card:hover .back-card {
  display: block;
  background-color: black;
  opacity: 0.8;
}
.back-card {
  display: none;
}
</style>