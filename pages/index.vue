<template>
  <div class="background-image">
    <Header />
  </div>
</template>

<script>
  import Header from './Header.vue'
  export default{
    components: {Header}
  }
</script>
  


<style>

body, .vsc-initialized{
  margin: 0!important;
}
.page-enter-active,
.page-leave-active {
  transition: opacity 0.5s;
}
.page-enter,
.page-leave-to {
  opacity: 0;
}
/* .background-image{
    background-image: url('./game/images/img1.jpg');
    width: 100%;
    height: 100%;
    background-size: cover; 
    background-repeat: no-repeat;
} */
</style>
