<template>
  <div>
     <div class="overviewdetail4   text-center mx-auto  jutify-center ">


  <div v-for="credit in credits.slice(0,count)"
            :key="`${credit.id} ${credit.credit_id}`"
            class="mx-auto     flex flex-col"
          >
        <router-link :to="`/moviedetails/${credit.id}/`">
        <div class="personsall">    <img
                v-if="credit.poster_path"
                :src="`https://image.tmdb.org/t/p/w500/${credit.poster_path}`"
                class="profileimage"
                id="profileimage"
              />
          </div> 
            </router-link>

<div v-if="credit.poster_path" class="profile-name ">

  {{  credit.name || credit.character }}
</div>
          </div>  
          </div>
    <div
    v-if="datacount > 16 "
    @click="count += 8"
     class="see justify-center text-center mx-auto flex my-5 bg-red-400 px-4 py-2 cursor-pointer font-bold  rounded">
     Show More
     <i class="fas fa-caret-down ml-1 my-auto"></i>
     
     </div>

<skeleton v-if="loading"> </skeleton>
  </div>
</template>

<script>
import axios from "axios"
import skeleton from "./skeleton"

export default {

     data() {
    return {
    count: 16,
      loading: true,
         credits: '',
         datacount:'',


}},

 components:{
    skeleton,
  },

methods: {
        async getCredits() {
      const res = await axios.get(
        `https://api.themoviedb.org/3/person/${this.$route.params.id}/movie_credits?api_key=cffed36e338abe3170a6f5872e6b2de6&language=en-US`
      )
      this.credits = res.data.cast
      this.loading = false
        this.datacount = res.data.cast.length
    
    },
},

 mounted() {
      this.getCredits();
      
  },
}
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


.overviewdetail4 {
  padding: 20px 10px;
  text-align: center;
  display: flex;
  flex-wrap: wrap;
  // background: linear-gradient(90deg, rgba(129, 24, 24, 0.65)  0%, rgba(212, 82, 82, 0.65)  50%, rgba(228, 10, 10, 0.65) 100%);
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


.profile-name {
    font-family: "Do Hyeon", sans-serif;
  letter-spacing:1px;
  font-size:12px;
    text-shadow: 0px 2px 0px $darkcolor;
    cursor:pointer;
    max-width:96px;
}

.see {
    font-family: "Do Hyeon", sans-serif;
  letter-spacing:1px;
  font-size:16px;
    text-shadow: 0px 2px 0px $darkcolor;
    cursor:pointer;
    background-color: $lightcolor;
        min-width: 100%;
}




@keyframes slaceleft {
  0% {transform:translateX(0) }
  100% {transform:translateX(-500px) 
  
  }
  
}

</style>