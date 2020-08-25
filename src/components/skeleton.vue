<template>
  <div class="skeletoncredit text-center mx-auto justify-center">
    <div
      class=" justify-center items-center text-center mx-auto flex flex-col"
      v-for="skeletoncount in 16"
      :key="skeletoncount"
    >
      <div class="skeletongray mx-auto"></div>

      <div class="s-profile-name mx-auto"></div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss">
$lightercolor: #f6b1c3;
$lightcolor: #f0788c;
$normalcolor: #de264c;
$darkcolor: #bc0d35;
$darkercolor: #a20d1e;
$radius: 10px;
$margin: 10px;
$shadow: 2px 2px $normalcolor;

.skeletongray {
  min-width: 76px;
  min-height: 76px;
  max-width: 76px;
  max-height: 76px;
  border-radius: 50%;
  display:flex;
  margin: 10px;
  cursor: pointer;
  animation: placeholderShimmer 15s linear infinite;
  background-image: linear-gradient(
    to right,
    $lightcolor 0%,
    $lightercolor 50%,
    $lightcolor 100%
  );
}

.skeletoncredit {
    padding: 20px 10px;
  padding-bottom: 10px;
  text-align: center;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  animation: placeholderShimmer 15s linear infinite;
}

.s-profile-name {
  max-width: 76px;
  min-width: 76px;
  background-image: linear-gradient(
    to right,
    $lightcolor 0%,
    $lightercolor 50%,
    $lightcolor 100%
  );
  background-repeat: repeat;
  background-size: 76px 13px;
  height: 13px;
  border-radius: 10px;
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