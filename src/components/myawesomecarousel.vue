<template>
  <div >

    <div class="populartitles font-bold text-5xl ">Popular Movies</div>

<div>


    <div id="scrollbar-custom" class="pt-12 carouseltop">
     
      <div @mouseover="onMouseOver" @mouseleave="onMouseLeave"
        class="carouselimages flex flex-col mx-4 p-4"
        v-for="film in movie.slice(0,18)"
        :key="film"
      >
        <router-link :to="`/moviedetails/${film.id}/`">
          <img class="posterpost" :src="`https://image.tmdb.org/t/p/w500/${film.poster_path}`" />

          <div
            class="profile-name text-center my-auto items-center mx-auto"
          >{{ film.name || film.title }}</div>
        </router-link>
      </div>
    </div>

 <div class="flex rldiv justify-space">
      <button
       @click="scroll_left" class="lBtn">
        <i class="fas fa-chevron-left"></i>
      </button>
      <button
       @click="scroll_right" class="rBtn">
        <i class="fas fa-chevron-right"></i>
      </button></div>

</div>

    <theloading v-if="loading"> </theloading>
  </div>
</template>

<script>
import axios from "axios";
import theloading from "../components/theloading";

export default {
  data() {
    return {
      value: 4,
      val: 0,
      movie: "",
      loading: true,
      a: this.val,
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

    scroll_left() {
      let content = document.querySelector(".carouseltop");
      content.scrollLeft -= 848;
      this.val -= 1;
    },
    scroll_right() {
      let content = document.querySelector(".carouseltop");
      content.scrollLeft += 848;
    },
    scroll_lefter() {
      let content = document.querySelector(".carouseltop");
      content.scrollLeft -= 10000;
    },

    onMouseLeave(){
this.autoscroll();
    },
        onMouseOver(){
clearInterval(this.a)
    },

    autoscroll( ){
           this.a = setInterval(() => {
      this.scroll_right();
      this.val += 1;
      if (this.val === this.value) {
        let content = document.querySelector(".carouseltop");
        content.scrollLeft -= 20000;
        this.val = 0;
      }
    }, 3000);
     return this.a
    },
   
  },

  mounted() {
this.autoscroll();


    this.getpopmovies();
  },

    components:{
    theloading,
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

* {
  color: white;
  scroll-behavior: smooth;
}

.populartitles {
  color: white !important;
  display: flex;
  justify-content: center;
  box-shadow: inset 5em 5em rgba(246, 177, 195, 0.95);
  text-shadow: 3px 3px $normalcolor, 5px 5px $darkcolor;
  background-size: 250px;
  text-align: center;
  font-family: "Do Hyeon", sans-serif;
  letter-spacing: 15px;
  margin-top:100px;
  margin-bottom:50px;
}

.profile-name {
  font-family: "Do Hyeon", sans-serif;
  letter-spacing: 1px;
  font-size: 14px;
  text-shadow: 0px 2px 0px $darkcolor;
  cursor: pointer;
  max-width: 150px;
}

.carouseltop {
  display: flex;
  margin-bottom:100px;
  overflow-x: auto;
  overflow-y:hidden;
  background-image: linear-gradient(
    to right,
    $lightcolor 0%,
    $lightercolor 100%
  );
  background-repeat: repeat;
  background-size: 10px;
  box-shadow: 0 0 20px 5px $darkercolor;



  
}

.carouselimages {
  min-width: 180px;
  max-width:180px;
  cursor: pointer;
}

.posterpost {
  box-shadow: 0 0 15px 2px $darkcolor;

  display: flex;
  border-radius: $radius;
}

.carouselimages:hover {
  animation: scaleup 0.5s forwards;
}

.carouselimages:hover .posterpost {
  transition: 0.5s;
  box-shadow: 0 0 20px 5px $darkcolor;
}

@keyframes scaleup {
  0% {
    -webkit-transform: scale(1);

    transform: scale(1);
  }
  100% {
    -webkit-transform: scale(1.3);

    transform: scale(1.3);
  }
}

.lBtn {

  background-color: $darkcolor;
  color: white;
  background-color: $darkcolor;
  width: 75px;
  height: 75px;
  border-radius: 50%;
  font-size: 35px;
  font-weight: bold;
  opacity: 0.5 !important;

  outline: none !important;
  z-index: 2000;
}

.lBtn:hover {
  opacity: 1;
}
.rBtn:hover {
  opacity: 1;
}

.rBtn {
  background-color: $darkcolor;
  color: white;
  width: 75px;
  height: 75px;
  border-radius: 50%;
  font-size: 35px;
  font-weight: bold;
  opacity: 0.5 !important;
  outline: none !important;
  z-index: 2000;
  border:1
}

.rldiv {
  justify-content:space-between;
  padding:0 15px 0 15px;
  margin-top:-315px;
  z-index:1999;

}


#scrollbar-custom::-webkit-scrollbar{
		max-width:200px !important;
		background-color:$lightcolor;
    height:10px !important;
	}
	#scrollbar-custom::-webkit-scrollbar:vertical{
		height:10px;
 
	}
	#scrollbar-custom::-webkit-scrollbar-track:vertical{
		border:1px solid transparent;
		border-radius:10px;
    width:100px !important;
    height:100px;

	}
	#scrollbar-custom::-webkit-scrollbar-thumb{
		background-color:$darkcolor;
		border:1px solid transparent;
		border-radius:16px;
	}
	#scrollbar-custom::-webkit-scrollbar-thumb:hover{
		background-color:$darkercolor;
		border:1px solid transparent;
	}
	#scrollbar-custom::-webkit-scrollbar-thumb:active{
		background-color:$darkercolor;
		border:1px solid transparent;
	}
</style>