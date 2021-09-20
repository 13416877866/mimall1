<template>
  <div id="app">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <img alt="Vue logo" src="./assets/logo.png">
    {{age}}
  </div>  
</template>


<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios'

//vue-cli创建项目 mi-mall
//托管平台建立仓库 mall
//mi-mall git add. git commit -m '' git push ---> mall
//mi-mall开发 git add. git commit -m '' git push ---> mall

//git clone 仓库mall ---> 本地
export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data(){
    return {
      age:30
    }
  },
  mounted(){
    let url="https://www.imooc.com/common/adver-getadverlistbymarking"
    axios.get(url).then(()=>{
      
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;}
</style>
