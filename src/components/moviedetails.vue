<template>
  <div>
    <div
      :style="`background:url(https://image.tmdb.org/t/p/original${backgroundImage()});` "
      class="bum grid grid-cols-1 md:flex mx-auto justify-center text-center"
    >
      <div class="overviewdetail none1 w-5/12 flex flex-col">
        <div v-if="movie.overview"  class="title3 font-bold text-2xl">Overview</div>
        <div class="overview">{{movie.overview}}</div>

        <div class="title3 font-bold text-2xl">Genres</div>
        <div :key="genre.id" v-for="genre in movie.genres" class="overview">{{genre.name}}</div>

        <div v-if="movie.homepage" class="title3 font-bold text-2xl">Homepage</div>
        <div class="overview text-center">
          <a target="_blank" class="text-center" :href="`${movie.homepage}`">{{movie.homepage}}</a>
        </div>

        <div  class="title3 font-bold text-2xl">Production Companies</div>
        <div class="yeyo mb-4">
          <div
            :key="company.id"
            v-for="company in movie.production_companies"
            class="justify-center mx-auto"
          >
            <img
              v-if="company.logo_path"
              :src="`https://image.tmdb.org/t/p/original${company.logo_path}` "
              class="profileimage2 mx-auto"
            />

            <img
              v-else
              :src="`https://via.placeholder.com/500x500.png/a20d1e/f6b1c3/d9dedb?text=${company.name}`"
              class="profileimage3 -cover mx-auto"
            />

            <div class="profile-name">{{company.name}}</div>
          </div>
        </div>
      </div>

      <div class="overviewdetail2 w-2/12 hidden">
        <div class="imageboxx mx-auto">
          <div class="populartitle2 font-bold text-2xl">{{movie.title || movie.name}}</div>
<div
>
<div v-if="isFocused"
@click="onblur"
 class="modalim">
 <span
 @click="onblur"
  class="cursor-pointer font-bold text-3xl closerr">X  </span>
  </div>
  <div 
  
  :class="[isFocused ? 'topdiv' : 'hiddens']"
  >
<img 
 class="m-auto"
  :class="[isFocused ? 'imageall' : 'hiddens']"
                :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
/> </div>

        <img 
   @click="onclick"   
         v-if="movie.poster_path"
                :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
            class="detailsimage cursor-pointer w-64"
              />
    <img
              v-else
              :src="`https://via.placeholder.com/500x700.png/a20d1e/f6b1c3/d9dedb?text=${movie.name || movie.title}`"
              class="detailsimage cursor-pointer w-64"
            />


           </div>
          <div class="flex-col text-center mt-2 mb-auto">
            <div class="desc2">
              <i class="fas fa-calendar-day mr-1"></i>
              Release Date: {{movie.release_date}}
            </div>

            <div class="desc2">
              <i class="fas fa-heart mr-1"></i>
              Vote Average:
              {{movie.vote_average}}
            </div>

            <div class="desc2">
              <i class="fas fa-fire-alt mr-1"></i>
              Popularity:
              {{movie.popularity}}
            </div>
            <div class="desc2 flex flex-wrap">
              <i class="fas fa-globe mr-1"></i> Languages:
              <div :key="lang.id" v-for="lang in movie.spoken_languages" class="mx-1">{{lang.name}}</div>
            </div>
          </div>
        </div>
      </div>

      <div class="overviewdetail none2 flex flex-col">
        <div class="title3 font-bold text-2xl">Overview</div>
        <div class="overview">{{movie.overview}}</div>
      </div>
      <div class="overviewdetail3 justify-center flex-col w-1/1 md:w-5/12">
        <div class="title3 font-bold text-2xl">Credits</div>
        <div class="overviewdetail4 flex  text-center mx-auto  jutify-center ">
          <div
             class="mx-auto  items-center flex flex-col"
            v-for="credit in credits.slice(0,count)"
            :key="credit.id + credit.cast_id"
          >
            <router-link  :to="`/persondetails/${credit.id}/${credit.name}`">
             
             <div class="personsall grid-cols-1  grid">
              <img
                v-if="credit.profile_path"
                :src="`https://image.tmdb.org/t/p/w500/${credit.profile_path}`"
                class="profileimage    "
              />
              <img
                v-else
                :src="`https://via.placeholder.com/500x700.png/a20d1e/f6b1c3/d9dedb?text=${credit.name}`"
                class="profileimage "
              />

              <div class="profile-name">{{ credit.name }}</div>
         </div>   </router-link>
          </div>
          
          <skeleton v-if="loading"> </skeleton>
       
              <div
    v-if="datacount > 16 "
    @click="count += 8"
         class="see justify-center text-center mx-auto flex my-5 bg-red-400 px-4 py-2 cursor-pointer font-bold  rounded">
   Show More
     <i class="fas fa-caret-down ml-1 my-auto"></i>
     
     </div>
        </div>
        <div class="mx-auto">
          <div  class="title3 mx-auto font-bold text-2xl">Trailer</div>
            <iframe
           
     
              class="my-3 h-40 mx-auto  trailer"
              v-for="video in videos.slice(0,1)"
              :key="video.id "
              :src="`https://www.youtube.com/embed/${video.key}`"
            >
            </iframe>
        </div>
      </div>
    </div>

    <theloading v-if="loading"></theloading>
  </div>
</template>

<script>
import axios from "axios";
import theloading from "./theloading";
import skeleton from "./skeleton";


export default {
  data() {
    return {
      movie: "",
      loading: true,
      credits: "",
      videos: "",
      isFocused:false,
         count: 16,
                 datacount:'',
    };
  },

  components: {
    theloading,
    skeleton,
  },

  methods: {

    onclick() {
      console.log("click");
         this.isFocused=true
    },
    onblur() {
      console.log("blur");
         this.isFocused=false
    },

    async getopmovies() {
      const movie = await axios.get(
        `https://api.themoviedb.org/3/movie/${this.$route.params.id}?api_key=cffed36e338abe3170a6f5872e6b2de6&language=en-US`
      );
      this.movie = movie.data;
      this.loading = false;
    },
    backgroundImage() {
      return this.movie.backdrop_path;
    },

    async getCredits() {
      const res = await axios.get(
        `https://api.themoviedb.org/3/movie/${this.$route.params.id}/credits?api_key=cffed36e338abe3170a6f5872e6b2de6`
      );
      this.credits = res.data.cast;
      this.loading = false;
          this.datacount = res.data.cast.length
    },
    async getVideos() {
      const res = await axios.get(
        `https://api.themoviedb.org/3/movie/${this.$route.params.id}/videos?api_key=cffed36e338abe3170a6f5872e6b2de6&language=en-US`
      );
      this.videos = res.data.results;
      this.loading = false;
    },
  },

  mounted() {
    this.getopmovies();
    this.getCredits();
    this.getVideos();
  },
};
</script>

<style lang="scss" >
$lightercolor: #f6b1c3;
$lightcolor: #f0788c;
$normalcolor: #de264c;
$darkcolor: #bc0d36;
$darkercolor: #a20d1e;
$radius: 10px;
$margin: 10px;
$shadow: 2px 2px $normalcolor;

.bum {
  border: solid 10px $lightercolor;
  background-size: cover !important;
  background-position: center !important;
  background-repeat: no-repeat;
  outline: 5px dashed $lightcolor;
  outline-offset: -8px;
  margin-top: -4px;
  color: white;
  justify-content: center;
}

.hidden {
  width: 330px !important;
}

iframe:hover {
  z-index:2000;
  position:fixed;
  top:5%;
  right:5%;
  width:90%;
  height:90%;
  box-shadow:0 0 0 2px white, 0 0 0 4px $lightcolor, 0 0 500px 500px rgba(0, 0, 0, 0.8);
}

.none2 {
  display: none !important;
  border-bottom: dashed 5px $lightcolor;
  padding-bottom: 25px !important;
}



.see {
    font-family: "Do Hyeon", sans-serif;
  letter-spacing:1px;
  font-size:16px;
    text-shadow: 0px 2px 0px $darkcolor;
    cursor:pointer;
    min-width: 100%;
    background-color: $lightcolor;
}






@media only screen and (max-width: 950px) {
  .hidden {
    width: 100% !important;
    border-bottom: dashed 5px $lightcolor;
  }

  .none1 {
    display: none !important;
  }

  .none2 {
    display: flex !important;
  }
}

.imageboxx {
  display: flex;
  flex-direction: column;

  padding: 60px 0;
  overflow: hidden;
  justify-content: center;
  text-align: center;
  border-right: 5px dashed $lightcolor;
  border-left: 5px dashed $lightcolor;
  max-width: 330px;
  min-width: 330px;
  align-items: center;
  background-color: $lightercolor;
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
  letter-spacing: 10px;
  margin-bottom: 35px;
  max-width: 300px;
}

.title3 {
  color: white !important;
  display: flex;
  justify-content: center;

  text-shadow: 3px 3px $normalcolor, 5px 5px $darkcolor;
  text-align: center;
  font-family: "Do Hyeon", sans-serif;
  letter-spacing: 10px;
  padding: 25px;
  padding-bottom: 10px;
}

.overview {
  text-align: center;
  font-family: "Do Hyeon", sans-serif;
  letter-spacing: 3px;
  text-shadow: 0px 2px 0px $darkcolor;
  padding: 0px 25px;
  justify-content: center;
  max-width: 450px;
  overflow: hidden;
  margin-right:auto;
  margin-left:auto;
}

.detailsimage {
  border-radius: $radius;
}





.overviewdetail {
  text-align: center;
  padding:0 !important;
  display: flex;
  background: rgb(240, 120, 140);
  // background: linear-gradient(90deg, rgba(129, 24, 24, 0.65)  0%, rgba(212, 82, 82, 0.65)  50%, rgba(228, 10, 10, 0.65) 100%);
  background: rgba(0, 0, 0, 0.5);
}

.overviewdetail3 {
  padding: 0px 10px;
  text-align: center;
  background: rgb(240, 120, 140);
  display:flex;
  
  // background: linear-gradient(90deg, rgba(129, 24, 24, 0.65)  0%, rgba(212, 82, 82, 0.65)  50%, rgba(228, 10, 10, 0.65) 100%);
  background: rgba(0, 0, 0, 0.5);
}

.overviewdetail4 {
  padding: 20px 10px;
  text-align: center;
  display: flex;
  flex-wrap: wrap;
  // background: linear-gradient(90deg, rgba(129, 24, 24, 0.65)  0%, rgba(212, 82, 82, 0.65)  50%, rgba(228, 10, 10, 0.65) 100%);
}

.overviewdetail2 {
  justify-content: center;
  text-align: center;
  display: flex;
  width: 100%;
  //   background: rgb(240,120,140);
  // background: linear-gradient(90deg, rgba(222,38,76,0.65) 0%, rgba(246,177,195,0.65) 50%, rgba(222,38,76,0.65) 100%);
  background: rgba(0, 0, 0, 0.5);
}

.yeyo {
  display: flex;
  flex-wrap: wrap;
}
.desc2 {
  margin-top: 15px;
  color: white !important;
  justify-content: center;
  text-shadow: 1px 1px 5px $normalcolor;
  text-align: center;
  font-family: "Do Hyeon", sans-serif;
  letter-spacing: 3px;
  padding: 0 7px;
}
.profileimage {
  min-width: 76px;
  min-height: 76px;
  max-width: 76px;
  max-height: 76px;
  object-fit: cover;
  border-radius: 50%;
  margin: 10px;
  cursor: pointer;
  box-shadow: 0 0 0 2px white, 0 0 0 4px $lightcolor;
}




@keyframes slaceleft {
  0% {transform:translateX(0) }
  100% {transform:translateX(-500px) 
  
  }
  
}

.profileimage2 {
  min-width: 76px;
  min-height: 76px;
  max-width: 76px;
  max-height: 76px;
  object-fit: contain;
  border-radius: 50%;
  margin: 10px;
  cursor: pointer;
  box-shadow: 0 0 0 2px white, 0 0 0 4px $lightcolor;
}

.trailer {
   box-shadow: 0 0 0 2px white, 0 0 0 4px $lightcolor;
   border-radius:$radius;
   margin-bottom:35px;
}

.profileimage3 {
  min-width: 76px;
  min-height: 76px;
  max-width: 76px;
  max-height: 76px;
  object-fit: cover;
  border-radius: 50%;
  margin: 10px;
  cursor: pointer;
  box-shadow: 0 0 0 2px white, 0 0 0 4px $lightcolor;
}
.profileimage:hover {
  box-shadow: 0 0 0 2px white, 0 0 5px 4px $darkcolor;
}

.profile-name {
  font-family: "Do Hyeon", sans-serif;
  letter-spacing: 1px;
  font-size: 12px;
  text-shadow: 0px 2px 0px $darkcolor;
  cursor: pointer;
  max-width: 96px;
}



.closerr {
  position:fixed;
  right:5%;
  top:2%;
  color: white;
  text-shadow:$shadow;
  border:2px white solid;
min-width:50px;
min-height:50px;
background-color:$lightcolor;
  border-radius:50%;
}

.imageall {  
 z-index:2000;   
    position:fixed;
height:90%;
  border-radius:$radius; 
  top:5%;
}

@media only screen and (max-width: 560px) {
.imageall {
  height:70%;
  top:15%;
}
}




.topdiv {
  display:flex;
  justify-content: center;
  align-items: center;
}

.hiddens {
  display:none;
}

.modalim {
  position:fixed;
  left:0; 
  top:0;
  width:100%;
  height:100%;
  background-color:rgba(0, 0, 0, 0.8);
  z-index:1500
}

</style>