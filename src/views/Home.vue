<template>
  <div >
    
      <div class="populartitle font-bold text-5xl mt-12">Popular Movies  

      </div>

      <div class="movieshow grid  lg:grid-cols-4 grid-cols-1 md:grid-cols-2 gap-6">

<div v-for="film in movie" :key="film" >
 <div  class="mt-12 mx-auto moviecomp">

   <div class="movietitle">

  {{film.name || film.title }}
</div>

<img class="movieposter w-48 " :src="`https://image.tmdb.org/t/p/original${film.poster_path}` ">
   <div class="movietitle">
<i class="fas fa-calendar-day mr-2"></i>
  {{film.first_air_date || film.release_date}}  
</div>






 </div>

 <div class="flex justify-center text-center items-center" >

   <div class="desc">
<i class="fas fa-heart "></i>

  {{film.vote_average}} 

</div>

   <div class="desc">
  <i class="fas fa-fire-alt"></i>

  {{film.popularity}}
</div>

</div>

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
      loading:true,
    };
  },

  methods: {
    async getpopmovies() {
      const bok = await axios.get(
        "https://api.themoviedb.org/3/trending/all/week?api_key=cffed36e338abe3170a6f5872e6b2de6"
      );
      this.movie=bok.data.results
      this.loading=false
    },
},

   mounted() {
      this.getpopmovies();
    },

};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Do+Hyeon&display=swap');

$lightercolor: #F6B1C3;
$lightcolor: #F0788C;
$normalcolor: #DE264C;
$darkcolor: #BC0D35;
$darkercolor: #A20D1E;
$radius: 10px;
$margin: 10px;
$shadow: 2px 2px $normalcolor;

html {
  margin: 0 0 100px;

}

body {
  background-color: $normalcolor;
  
}

.populartitle {
  color: white !important;
  display:flex;
  justify-content: center;
  background: $lightercolor url("https://svgsilh.com/svg/331553.svg")    ;
box-shadow: inset 5em 5em rgba(255, 163, 198, 0.95);
text-shadow: 3px 3px $normalcolor, 5px 5px $darkcolor;
  background-size: 250px;
text-align: center;
font-family: 'Do Hyeon', sans-serif;
letter-spacing: 15px;

}

.moviecomp {
  background-color: $darkcolor;
padding: 15px 25px;
border-radius:10px 10px 0 0;
width:15.5rem !important;
display:flex;
flex-direction: column;
align-items: center;
text-align: center;

min-height: 400px;
max-height:400px;

-webkit-box-shadow: 0px 5px 0px 5px $darkercolor;
-moz-box-shadow: 0px 5px 0px 5px $darkercolor;
box-shadow: 0px 5px 0px 5px $darkercolor;
}

.movieposter {
  border-radius: $radius;

}

.movietitle {
  display:flex;
  text-align: center;
  justify-content: center;
  align-items: center;
  align-self: center;
  color:$lightercolor;
  font-weight: bold;
  letter-spacing: 1px;
  font-size: 15px;
  margin-bottom: $margin;
  min-height: 40px;
  max-height:40px;
text-shadow: $shadow;

}

.desc {
 color:$lightercolor;
 margin:0px 34px;
  font-weight: bold;
  letter-spacing: 1px;
  font-size: 12px;
padding:10px 0px;
border-radius:0 0 10px 10px;
min-width:90px !important;
text-shadow: $shadow;
background-color:$darkcolor;
-webkit-box-shadow: 0px 5px 0px 5px $darkercolor;
-moz-box-shadow: 0px 5px 0px 5px $darkercolor;
box-shadow: 0px 5px 0px 5px $darkercolor;
}


</style>