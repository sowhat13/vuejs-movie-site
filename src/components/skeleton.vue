<template>


   <div class="skeletoncredit text-center mx-auto justify-center px-5">

<div v-for="skeletoncount in 8"
:key="skeletoncount"
>
 <div class="skeletongray "> 
  
 </div>

<div class="s-profile-name mx-auto ">

</div>

</div>




</div>
</template>

<script>
export default {

}
</script>

<style lang="scss">

$lightercolor: #F6B1C3;
$lightcolor: #F0788C;
$normalcolor: #DE264C;
$darkcolor: #BC0D35;
$darkercolor: #A20D1E;
$radius: 10px;
$margin: 10px;
$shadow: 2px 2px $normalcolor;

.skeletongray {
  min-width:76px;
  min-height:76px;
   max-width:76px;
  max-height:76px;
  object-fit: cover;
  border-radius:50%;
  margin:10px;
cursor:pointer;
   animation: placeholderShimmer 15s linear infinite;
    background-image: linear-gradient(
    to right,
      $lightcolor 0%,
    $lightercolor 50%,
    $lightcolor 100%,
  );
}

.skeletoncredit {
    padding-bottom:10px;
    text-align: center;
    display:flex;
    flex-wrap: wrap;
    
       animation: placeholderShimmer 15s linear infinite;
}

.s-profile-name {
  
    max-width:76px;
    min-width: 76px;
  background-image: linear-gradient(
    to right,
    $lightcolor 0%,
    $lightercolor 50%,
    $lightcolor 100%,
  );
  background-repeat: repeat;
  background-size: 76px 13px;
    height:13px;
    border-radius:10px;
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