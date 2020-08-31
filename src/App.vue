<template>
  <div >
   

    <div class="curtain-container">
    <div class="curtain-panel">
 
      <div class="left-curtain curtain" data-title="WELCOME"></div>
      <div class="right-curtain curtain" data-title="WELCOME"></div>
    </div>
  </div>

    <div class="netnav " id="nav">
      <router-link to="/">Home</router-link> 
     <router-link to="/">  <img class="logo" src="https://3.bp.blogspot.com/-YjTqvcnZHZw/WmMRgRH9_WI/AAAAAAAABxo/hGQxNeDPLoMXyzBWiI8r7vrdvbYcnQ2UACLcBGAs/s1600/cinemaximum-logo.png" >
    </router-link> 
      <router-link to="/Carousel">Carousel</router-link>
    </div>

    <transition name="fade">
    <router-view/>
  </transition>

  
  </div>
</template>
<script>
export default {
  
}
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




.curtain-container {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  z-index: 2000 !important;
  font-size: 100px;
  font-weight: bold;
  color: white;
 pointer-events: none;
animation: disnone 0.01s forwards;
animation-delay: 2.9s;
  text-shadow: $shadow;
font-family: 'Do Hyeon', sans-serif;
letter-spacing: 15px;
}

.curtain-panel {
  display: flex;
  height: 120%;
  width: 100%;
  overflow: hidden;
  z-index: 2000 !important;

 pointer-events: none;
animation: disnone 0.01s forwards;
animation-delay: 2.9s;

}

.curtain-panel .curtain {
  width: 50%;
    background-image: linear-gradient(
    to right,
    $lightcolor 0%,
    $lightercolor 100%
  );
  background-repeat: repeat;
  background-size: 25px;
  position: relative;
 pointer-events: none;
  display: flex;
  align-items: center;
  overflow: hidden;
  box-shadow:inset 0 0 10px 3px rgba(126, 11, 38, 0.9),0px 0px 250px 5px rgba(0,0,0, 0.5);
  z-index: 2000 !important;
}



.right-curtain {
  animation:slide-right 2.5s forwards;
  animation-delay: 0.5s;
 pointer-events: none;
  z-index: 2000 !important;


}

.left-curtain {
  animation:slide-left 2.5s forwards;
  animation-delay: 0.5s;
 pointer-events: none;
  z-index: 2000 !important;

}

.curtain-panel .curtain:before {
  content: attr(data-title);
  text-align: center;
  width: 200%;
  position: absolute;
  top: 40%;
  z-index: 2000 !important;

  line-height: 0;
 pointer-events: none;
text-shadow: 3px 3px $normalcolor, 5px 5px $darkcolor;

}

.curtain-panel .left-curtain:before {
  left: 0;
   pointer-events: none;
}

.curtain-panel .right-curtain:before {
   pointer-events: none;
  right: 0;
}




@keyframes slide-left {
  0% {
    background-position: -100px 0;
  }
  100% {
      transform: translateX(calc(-100% - 2rem ));
          background-position: -200px 0;
  }
}

@keyframes slide-right {
  0% {
  background-position: -100px 0;
  }
  100% {
      transform: translateX(calc(100% ));
          background-position: 200px 0;
  }
}

@keyframes disnone {
  0% {}

  100% {width:0px;
  height:0px;
  }
}

@media only screen and (max-width: 1025px) {
  .netnav {
    font-size:12px;

     a {
   color:White;
   text-decoration:none;
   margin:20px 10px !important;
   text-shadow: 1px 1px $normalcolor, 3px 3px $darkcolor;
font-family: 'Do Hyeon', sans-serif;
letter-spacing: 3px;
font-size: 12px !important;
text-transform:uppercase;
font-weight: bold;
margin:auto 10px;

 }

img{
  padding:12px;
  background-color:$lightercolor;
  max-width: 120px !important;
  min-height: 60px !important;
  border-radius:0 0 50% 50%;
 box-shadow: 0 10px 0px -5px $lightcolor, 0 14px 0px -7px $darkcolor,  0 20px 5px -10px $darkercolor;;
margin:auto auto;
}
  }
}

.netnav {background-color: $lightercolor;
box-shadow: 0px 0px 0px 5px $lightcolor, 0 0 0px 7px $darkcolor, 0 0 5px 10px $darkercolor;
display:flex;
padding-top:7px;
padding-left:5%;
width: 100%;
z-index: 1020 !important;
text-align: center;
max-height:50px;
position:relative;
top:0;
justify-content: center;

* {
  z-index: 1020 !important;
}

 a {
   color:White;
   text-decoration:none;
   text-shadow: 1px 1px $normalcolor, 3px 3px $darkcolor;
font-family: 'Do Hyeon', sans-serif;
letter-spacing: 5px;
font-size: 20px;
text-transform:uppercase;
font-weight: bold;
 }

img{
  padding:15px;
  background-color:$lightercolor;
  max-width: 180px;
  min-height: 90px;
  border-radius:0 0 50% 50%;
 box-shadow: 0 10px 0px -5px $lightcolor, 0 14px 0px -7px $darkcolor,  0 20px 5px -10px $darkercolor;;
}

}


</style>
