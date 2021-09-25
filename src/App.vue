<template>
  <div id="app">
    <router-view></router-view>
  </div>  
</template>


<script>
//index可以省略
//import storage from './storage/index'
//vue-cli创建项目 mi-mall
//托管平台建立仓库 mall
//mi-mall git add. git commit -m '' git push ---> mall
//mi-mall开发 git add. git commit -m '' git push ---> mall
//git clone 仓库mall ---> 本地
export default {
  name: 'App',
  components: {
   
  },
  data(){
    return {
     res:{}
    }
  },
  mounted(){
  //本地加载请求静态json文件的形式
   this.axios.get('/mock/user/login.json').then((res)=>{
     this.res=res;
   });
 
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
