<template>
  <div>


      <div
           :style="`background:url(https://image.tmdb.org/t/p/original${backgroundImage()});background-size:cover` "
       class="bum grid grid-cols-1 md:flex mx-auto justify-center text-center ">
 
          <div class="overviewdetail none1  flex flex-col ">
            
             <div class="title3 font-bold  text-2xl">Overview</div>
<div class="overview ">
  {{movie.overview}}
</div>




           <div class="title3 font-bold  text-2xl">Genres</div>
<div
    :key="genre.id"
            v-for="genre in movie.genres"
 class="overview">
  {{genre.name}}
</div>

          </div>


 <div class="overviewdetail2 hidden">
    <div class="imageboxx mx-auto ">
    <div class="populartitle2 font-bold text-2xl">{{movie.title || movie.name}}</div>


           <img
              class="detailsimage  w-64"
              :src="`https://image.tmdb.org/t/p/original${movie.poster_path}` "
            />

<div class="flex-col text-center mb-auto">
                     <div class="desc2">
              <i class="fas fa-calendar-day mr-1"></i>
             Release Date: {{movie.release_date}}
            </div>

            <div class="desc2">
              <i class="fas fa-heart"></i>
Vote Average:
              {{movie.vote_average}}
            </div>

            <div class="desc2">
              <i class="fas fa-fire-alt"></i>
              Popularity:
              {{movie.popularity}}
            </div>
   </div>
   </div>
   </div>

        <div class="overviewdetail none2 flex flex-col ">
            
             <div class="title3 font-bold  text-2xl">Overview</div>
<div class="overview ">
  {{movie.overview}}
</div>




           <div class="title3 font-bold  text-2xl">Genres</div>
<div
    :key="genre.id"
            v-for="genre in movie.genres"
 class="overview">
  {{genre.name}}
</div>

          </div>
   
          <div class="overviewdetail">sdasdfsadf</div>
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
    async getopmovies() {
      const movie = await axios.get(`https://api.themoviedb.org/3/movie/${this.$route.params.id}?api_key=cffed36e338abe3170a6f5872e6b2de6&language=en-US`);
      this.movie = movie.data
      this.loading = false;
    },
  backgroundImage() {
    
      return this.movie.backdrop_path
    },

  },

  mounted() {
    this.getopmovies();
  },
};
</script>

<style lang="scss">

$lightercolor: #f6b1c3;
$lightcolor: #f0788c;
$normalcolor: #de264c;
$darkcolor: #bc0d36;
$darkercolor: #a20d1e;
$radius: 10px;
$margin: 10px;
$shadow: 2px 2px $normalcolor;

.bum {
    border:solid 10px $lightercolor;

background-position: center;
background-repeat: no-repeat;
    outline:5px dashed $lightcolor;
    outline-offset: -8px;
margin-top:-4px;    
color:white;
justify-content:center;

}

.hidden {
  width:330px !important
}

.none2 {
  display:none !important;
   border-bottom: dashed 5px $lightcolor;
   padding-bottom:25px !important;
}

@media only screen and (max-width: 768px) {
 .hidden {
  width:100% !important;
  border-bottom: dashed 5px $lightcolor;
}

.none1 {
  display:none !important;
}

.none2 {
  display:flex !important;
}
}

.imageboxx {
display:flex;
flex-direction: column;

padding: 60px 0;
overflow:hidden;
justify-content: center;
text-align: center;
border-right:5px dashed $lightcolor;
border-left:5px dashed $lightcolor;
max-width: 330px;
min-width:330px;
align-items: center;
background-color:$lightercolor;

}


.populartitle2 {
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
  max-width:300px;


}

.title3{
    color: white !important;
  display: flex;
  justify-content: center;

  text-shadow: 3px 3px $normalcolor, 5px 5px $darkcolor;
  text-align: center;
  font-family: "Do Hyeon", sans-serif;
  letter-spacing: 10px;
padding:25px;
padding-bottom:10px;


}

.overview {
  text-align: center;
  font-family: "Do Hyeon", sans-serif;
  letter-spacing:3px;
    text-shadow: 0px 2px 0px $darkcolor;
padding:0px 25px
}

.detailsimage {
    border-radius: $radius;
}

.overviewdetail {
  padding:0 10px;
    text-align: center;
    display:flex;
width:100%;
  background: rgb(240,120,140);
background: linear-gradient(90deg, rgba(222,38,76,0.65) 0%, rgba(246,177,195,0.65) 50%, rgba(222,38,76,0.65) 100%);
 
}

.overviewdetail2 {
  justify-content: center;
    text-align: center;
    display:flex;
width:100%;
  background: rgb(240,120,140);
background: linear-gradient(90deg, rgba(222,38,76,0.65) 0%, rgba(246,177,195,0.65) 50%, rgba(222,38,76,0.65) 100%);
 
}

</style>