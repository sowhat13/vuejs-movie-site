<template>
  <div>


      <div class="flex bum">

          <div class="overviewdetail">sdasdfsadf</div>
      <div class="imageboxx">
    <div class="populartitle2 font-bold text-2xl">{{movie.title || movie.name}}</div>

           <img
              class="detailsimage mb-auto w-64"
              :src="`https://image.tmdb.org/t/p/original${movie.poster_path}` "
            />
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
      const bok = await axios.get(`https://api.themoviedb.org/3/movie/${this.$route.params.id}?api_key=cffed36e338abe3170a6f5872e6b2de6&language=en-US`);
      this.movie = bok.data
      this.loading = false;
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
    background:url("https://s1.filmmodu.org/uploads/movie/cover/9427/qVygtf2vU15L2yKS4Ke44U4oMdD.jpg");
background-size: cover;
background-position: center;
background-repeat: no-repeat;

    outline:5px dashed $lightcolor;
    outline-offset: -8px;
margin-top:-4px;    
color:white;
justify-content:center;
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

.detailsimage {
    border-radius: $radius;
}

.overviewdetail {
    justify-content: center;
    text-align: center;
    display:flex;
    background-color:black;
}


</style>