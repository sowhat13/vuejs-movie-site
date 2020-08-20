<template>
  <div class="home">
    <div class="populartitle font-bold text-5xl mt-20">Popular Movies</div>

    <div class="movieshow grid lg:grid-cols-4 grid-cols-1 md:grid-cols-2 gap-6">
      <div v-for="film in movie" :key="film">
        <router-link :to="`/moviedetails/${film.id}/${film.name || film.title }`" >
        <div class="moviesall shine">
          <div class="movietitle">{{film.name || film.title }}</div>
          <div class="mx-auto moviecomp">
            <img
              class="movieposter w-48"
              :src="`https://image.tmdb.org/t/p/original${film.poster_path}` "
            />
            <div class="movietitle2">
              <i class="fas fa-calendar-day mr-2"></i>
              {{film.first_air_date || film.release_date}}
            </div>
          </div>

          <div class="flex justify-center text-center items-center">
            <div class="desc">
              <i class="fas fa-heart"></i>

              {{film.vote_average}}
            </div>

            <div class="desc">
              <i class="fas fa-fire-alt"></i>
              {{film.popularity}}
            </div>
          </div>
          </div>
       </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      movie: "",
      loading: true,
    };
  },

  methods: {
    async getpopmovies() {
      const bok = await axios.get(
        "https://api.themoviedb.org/3/trending/movie/week?api_key=cffed36e338abe3170a6f5872e6b2de6"
      );
      this.movie = bok.data.results;
      this.loading = false;
    },
  },

  mounted() {
    this.getpopmovies();
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Do+Hyeon&display=swap");

$lightercolor: #f6b1c3;
$lightcolor: #f0788c;
$normalcolor: #de264c;
$darkcolor: #bc0d35;
$darkercolor: #a20d1e;
$radius: 10px;
$margin: 10px;
$shadow: 2px 2px $normalcolor;

html {
  margin: 0 0 100px;
  overflow-x: hidden;
}

body {
  background-color: $normalcolor;
  animation: turn2 5s;
}

.home {
  animation-name: turn;
  animation-duration: 5s;
}

.populartitle {
  color: white !important;
  display: flex;
  justify-content: center;
  box-shadow: inset 5em 5em rgba(246, 177, 195, 0.95);
  text-shadow: 3px 3px $normalcolor, 5px 5px $darkcolor;
  background-size: 250px;
  text-align: center;
  font-family: "Do Hyeon", sans-serif;
  letter-spacing: 15px;
  margin-bottom: 35px;
}

.moviesall {
  cursor: pointer;
  -moz-box-shadow: inset 0px 0px 5px 1px $darkercolor;
  box-shadow: inset 0px 0px 5px 1px $darkercolor;
  -webkit-box-shadow: inset 0px 0px 5px 1px $darkercolor;
  padding: 30px 0 30px 0px;
  border-radius: $radius;
  margin: 15px;
  z-index: 5;
}

.moviecomp {
  background-color: $darkcolor;
  padding: 15px 25px;

  padding-top: 5px;
  width: 15.5rem !important;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  cursor: pointer;

  min-height: 350px;
  max-height: 350px;
  border-top: dashed 0.5px $darkercolor;
  -webkit-box-shadow: inset 1px 5px 5px 1px $normalcolor,
    0px 3px 0px 3px $darkercolor;
  -moz-box-shadow: inset 1px 15px 15px 1px $normalcolor,
    0px 3px 0px 3px $darkercolor;
  box-shadow: inset 1px 15px 15px 2px $normalcolor, 0px 4px 0px 3px $darkercolor;
}

.movieposter {
  border-radius: $radius;
  margin-top: 5px;
}

.movietitle {
  display: flex;
  text-align: center;
  justify-content: center;
  align-items: center;
  align-self: center;
  color: $lightercolor;
  font-weight: bold;
  letter-spacing: 1px;
  font-size: 15px;
  min-height: 70px;
  max-height: 70px;
  text-shadow: $shadow;

  background-color: $darkcolor;
  padding: 15px 25px;

  border-radius: 10px 10px 0 0;
  width: 15.5rem !important;

  align-items: center;
  text-align: center;

  margin-right: auto;
  margin-left: auto;

  -webkit-box-shadow: inset 11px -1px 75px 10px $normalcolor,
    0px -3px 0px 3px $darkercolor;
  -moz-box-shadow: inset 11px -1px 75px 10px $normalcolor,
    0px -3px 0px 3px $darkercolor;
  box-shadow: inset 11px -1px 75px 10px $normalcolor,
    0px -1px 0px 3px $darkercolor;
  border-bottom: 3px $darkercolor dashed;

  cursor: pointer;
}

@keyframes turn {
  from {
    filter: brightness(0%);
  }
  to {
    filter: brightness(100%);
  }
}

@keyframes turn2 {
  from {
    background-color: black;
  }
  to {
    background-color: $normalcolor;
  }
}

@-webkit-keyframes cutup {
  0% {
    -webkit-transform: rotate(0);
    transform: rotate(0);
    -webkit-transform-origin: bottom right;
    transform-origin: bottom right;
  }
  100% {
    -webkit-transform: rotate(30deg);
    transform: rotate(30deg);
    -webkit-transform-origin: bottom right;
    transform-origin: bottom right;
  }
}

@keyframes cutup {
  0% {
    -webkit-transform: rotate(0);
    transform: rotate(0);
    -webkit-transform-origin: bottom right;
    transform-origin: bottom right;
  }
  100% {
    -webkit-transform: rotate(30deg);
    transform: rotate(30deg);
    -webkit-transform-origin: bottom right;
    transform-origin: bottom right;
  }
}

@keyframes scaleup {
  0% {
    -webkit-transform: scale(1);

    transform: scale(1);
  }
  100% {
    -webkit-transform: scale(1.05);

    transform: scale(1.05);
  }
}

.moviesall:hover .movietitle {
  animation: cutup 0.5s forwards;
}

.movietitle2 {
  display: flex;
  text-align: center;
  justify-content: center;
  align-items: center;
  align-self: center;
  color: $lightercolor;
  font-weight: bold;
  letter-spacing: 1px;
  font-size: 15px;
  margin-bottom: $margin;
  min-height: 40px;
  max-height: 40px;
  text-shadow: $shadow;
}

.desc {
  color: $lightercolor;
  margin: 0px 34px;
  font-weight: bold;
  letter-spacing: 1px;
  font-size: 12px;
  padding: 10px 0px;
  border-radius: 0 0 10px 10px;
  min-width: 90px !important;
  text-shadow: $shadow;
  background-color: $darkcolor;
  -webkit-box-shadow: inset 1px -5px 5px 0.5px $normalcolor,
    0px 3px 0px 3px $darkercolor;
  -moz-box-shadow: inset 1px -5px 5px 0.5px $normalcolor,
    0px 3px 0px 3px $darkercolor;
  box-shadow: inset 0px -16px 15px -1px $normalcolor,
    0px 3px 0px 3px $darkercolor;
}

.shine {
  background-image: linear-gradient(
    to right,
    $lightcolor 0%,
    $lightercolor 100%
  );
  background-repeat: repeat;
  background-size: 10px;
}

.shine:hover {
  animation: placeholderShimmer 15s linear infinite;
}

@keyframes placeholderShimmer {
  0% {
    background-position: -100px 0;
  }

  100% {
    background-position: 500px 0;
  }
}
</style>