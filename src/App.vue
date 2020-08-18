<template>
  <div >
    <div class="netnav" id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>

  </div>
</template>
<script>
export default {
  
}
</script>
<style lang="scss">


.netnav {background-color:black;
display:flex;
margin:0px;
padding:0px;
width: 100%;
z-index: 1020;

 a {
   color:White;
   text-decoration:none;
   margin: 15px;
 }
}


</style>
