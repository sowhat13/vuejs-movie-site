<template>
   <div class="loading text-center text-5xl text-white font-bold">
 <div class="load "> 
   
   Loading
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

.loading {
  position:fixed;
  display:flex;
  background:rgba(255, 54, 54, 0.5);
height:100%;
width:100%;
justify-content:center;
text-align: center;
align-items: center;
top:0;
left:0;
  z-index:1020 !important;
  pointer-events: none;

}

.load  {
   color: white !important;
  display: flex;
  justify-content: center;
  text-shadow: 3px 3px $normalcolor, 5px 5px $darkcolor;
  background-size: 250px;
  text-align: center;
  font-family: "Do Hyeon", sans-serif;
  letter-spacing: 15px;
  animation: letspacer 5s infinite both;
    pointer-events: none;
}

@keyframes letspacer {
  0%{letter-spacing:3px }
  25%{letter-spacing:15px}
    50%{letter-spacing:3px}
      75%{letter-spacing:15px}
        100%{letter-spacing:3px}

}


@keyframes opacity {
  0%{opacity:1}
  100% {opacity:0}
  
}

</style>