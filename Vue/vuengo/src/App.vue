<template>
<div id="app">
 <home-page></home-page>
</div>
</template>

<script>
import HomePage from './views/HomePage.vue'
export default {
  name: 'App',
  components:{
    HomePage
  }
}
</script>

<style>
@import '../node_modules/bulma';
.select, select{
  width:100%;
}
.card{
  margin-bottom:20px;
}
.done{
  opacity:0.3;
}
</style>
