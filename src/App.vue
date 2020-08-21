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
      <router-link to="/about">About</router-link>
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

   body {
      animation: ovrflw 5s;
    }

    @keyframes ovrflw {
      0% {
  overflow: hidden;
      }

       100% {
         overflow: auto;
       }
    }

.curtain-container {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  z-index: 1020;
  font-size: 100px;
  font-weight: bold;
  color: white;

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
  z-index: 1020;

animation: disnone 0.01s forwards;
animation-delay: 2.9s;
}

.curtain-panel .curtain {
  width: 50%;
 background: url("https://image.freepik.com/free-photo/red-curtain-fabric-background-texture_38678-2804.jpg");
  position: relative;

  display: flex;
  align-items: center;
  overflow: hidden;
  box-shadow:0px 0px 250px 5px rgba(0,0,0, 0.5);

}

.right-curtain {
  animation:slide-right 2.5s forwards;
  animation-delay: 0.5s;


}

.left-curtain {
  animation:slide-left 2.5s forwards;
  animation-delay: 0.5s;

}

.curtain-panel .curtain:before {
  content: attr(data-title);
  text-align: center;
  width: 200%;
  position: absolute;
  top: 40%;
  line-height: 0;

text-shadow: 3px 3px $normalcolor, 5px 5px $darkcolor;

}

.curtain-panel .left-curtain:before {
  left: 0;
}

.curtain-panel .right-curtain:before {
  right: 0;
}




@keyframes slide-left {
  0% {

  }
  100% {
      transform: translateX(calc(-100% - 2rem ));
  }
}

@keyframes slide-right {
  0% {

  }
  100% {
      transform: translateX(calc(100% ));
  }
}

@keyframes disnone {
  0% {}

  100% {width:0px;
  height:0px;
  }
}


.netnav {background-color: $lightercolor;
box-shadow: 0px 0px 0px 5px $lightcolor, 0 0 0px 7px $darkcolor;
display:flex;
margin:0px;
padding:0px;
width: 100%;
z-index: 1020 !important;
justify-content:center;
text-align: center;
max-height:50px;
position:relative;
top:0;

* {
  z-index: 1020 !important;
}

 a {
   color:White;
   text-decoration:none;
   margin: 15px;
   text-shadow: 1px 1px $normalcolor, 3px 3px $darkcolor;
font-family: 'Do Hyeon', sans-serif;
letter-spacing: 5px;
font-size: 20px;
text-transform:uppercase;
font-weight: bold;
margin:auto 20px;

 }

img{
  padding:15px;
  background-color:$lightercolor;
  max-width: 180px;
  min-height: 90px;
  border-radius:0 0 50% 50%;
 box-shadow: 0 10px 0px -5px $lightcolor, 0 14px 0px -7px $darkcolor;

}

}


</style>
