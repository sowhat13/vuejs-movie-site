<template>
  <div>

      <div
       class="bum grid grid-cols-1 md:flex mx-auto justify-center text-center ">
 
          <div class="overviewdetail none1 w-5/12  flex flex-col ">
                   <div class="title3 font-bold  text-2xl">Biography</div>
<div class="overview ">
  {{person.biography}}
</div>

          </div>


 <div class="overviewdetail2 w-2/12 hidden">
    <div class="imageboxx mx-auto ">
    <div class="populartitle2 font-bold text-2xl">{{person.name}}</div>

        <img
                :src="`https://image.tmdb.org/t/p/w500/${person.profile_path}`"
            class="detailsimage w-64"
              />
           
<div class="flex-col text-center  justify-center  mx-auto mt-2 mb-auto">
            <div class="desc2">
              <i class="fas fa-calendar-day mr-1"> </i>
             Birthday: {{person.birthday}}
            </div>
              <div class="desc2">
              <i class="fas fa-fire-alt mr-1"></i>
              Popularity:
              {{person.popularity}}
            </div>
    <div class="desc2 ">
              <i class="fas fa-map-marked mr-auto mr-1"></i> 
              Place Of Birth: 
              {{person.place_of_birth}}
            </div>
          

   </div>
   </div>
   </div>

        <div class="overviewdetail none2 flex flex-col ">
            
          <div class="title3 font-bold  text-2xl">Biography</div>
<div class="overview ">
  {{person.biography}}
</div>



          </div>
   <div class="overviewdetail3 justify-center  flex-col w-1/1 md:w-5/12">
        <div class="title3 font-bold text-2xl  ">Movies & <br> Character Names</div> 
<creditmovies> </creditmovies>

  </div>
  </div>



<theloading v-if="loading"> </theloading>

  </div>
</template>

<script>
import axios from "axios"
import theloading from "./theloading"
import creditmovies from "./creditmovies"


export default {
  data() {
    return {
      movie: "",
      loading: true,
person:'',
};
  },

   components:{
    theloading,
    creditmovies,
  },

  methods: {
    async getopmovies() {
      const movie = await axios.get(`https://api.themoviedb.org/3/movie/${this.$route.params.id}?api_key=cffed36e338abe3170a6f5872e6b2de6&language=en-US`);
      this.movie = movie.data
      this.loading = false;
    },




        async getPerson() {
      const res = await axios.get(
       `https://api.themoviedb.org/3/person/${this.$route.params.id}?api_key=cffed36e338abe3170a6f5872e6b2de6&language=en-US`
      )
      this.person = res.data
      this.loading = false
    },

  },

  mounted() {
       this.getPerson()
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
background-size:cover !important;
background-position:  center !important;
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
padding:0px 25px;
justify-content: center;
max-width:450px;
overflow:hidden;
margin:0px auto 0px auto;
}
  
.detailsimage {
    border-radius: $radius;
}

.overviewdetail {
  padding:0 10px;
    text-align: center;
    display:flex;
  background: rgb(240,120,140);
// background: linear-gradient(90deg, rgba(129, 24, 24, 0.65)  0%, rgba(212, 82, 82, 0.65)  50%, rgba(228, 10, 10, 0.65) 100%);
  background:rgba(0, 0, 0, 0.5)
}

.overviewdetail3 {
  padding:0px 10px;
    text-align: center;
  background: rgb(240,120,140);
// background: linear-gradient(90deg, rgba(129, 24, 24, 0.65)  0%, rgba(212, 82, 82, 0.65)  50%, rgba(228, 10, 10, 0.65) 100%);
  background:rgba(0, 0, 0, 0.5)
}

.overviewdetail4 {
  padding:20px 10px;
    text-align: center;
    display:flex;
    flex-wrap: wrap;
// background: linear-gradient(90deg, rgba(129, 24, 24, 0.65)  0%, rgba(212, 82, 82, 0.65)  50%, rgba(228, 10, 10, 0.65) 100%);
}

.overviewdetail2 {
  justify-content: center;
    text-align: center;
    display:flex;
width:100%;
//   background: rgb(240,120,140);
// background: linear-gradient(90deg, rgba(222,38,76,0.65) 0%, rgba(246,177,195,0.65) 50%, rgba(222,38,76,0.65) 100%);
 background:rgba(0, 0, 0, 0.5)
}

.yeyo {
  display:flex;
  flex-wrap: wrap;
}


.desc2 {
  margin-top:15px;
      color: white !important;
  justify-content: center;
  text-shadow: 1px 1px 5px $normalcolor;
  text-align: center;
  font-family: "Do Hyeon", sans-serif;
  letter-spacing: 3px;
  padding:0 7px;
}

.profileimage {
  min-width:76px;
  min-height:76px;
   max-width:76px;
  max-height:76px;
  object-fit: cover;
  border-radius:50%;
  margin:10px;
cursor:pointer;
  box-shadow: 0 0 0 2px white, 0 0 0 4px $lightcolor;
}


.profileimage2 {
  min-width:76px;
  min-height:76px;
   max-width:76px;
  max-height:76px;
  object-fit: contain;
  border-radius:50%;
  margin:10px;
cursor:pointer;
  box-shadow: 0 0 0 2px white, 0 0 0 4px $lightcolor;
}

.profileimage3 {
  min-width:76px;
  min-height:76px;
   max-width:76px;
  max-height:76px;
  object-fit: cover;
  border-radius:50%;
  margin:10px;
cursor:pointer;
  box-shadow: 0 0 0 2px white, 0 0 0 4px $lightcolor;
}
.profileimage:hover {
 box-shadow: 0 0 0 2px white, 0 0 5px 4px $darkcolor;}

.profile-name {
    font-family: "Do Hyeon", sans-serif;
  letter-spacing:1px;
  font-size:12px;
    text-shadow: 0px 2px 0px $darkcolor;
    cursor:pointer;
    max-width:96px;
}
</style>