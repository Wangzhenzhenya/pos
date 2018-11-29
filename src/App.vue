<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <leftview></leftview>
    <div class="main">
       <router-view/>
    </div>
   
  </div>
</template>

<script>
import leftview from '@/components/common/leftview'
import pos from '@/components/page/pos'
export default {
  name: 'App',
  components:{
    leftview,pos
  }
}
</script>

<style>
#app {
  font-family: 'Microsoft YaHei','Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}

.main {
  float: left;
  width: 95%;
  background-color: rgb(247, 242, 232);
  overflow: hidden;
  height: 100%;
}
</style>
