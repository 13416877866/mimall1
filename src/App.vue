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
    
    }
  },
  mounted(){
      this.getUser();
      this.getCartCount();
   },
   methods:{
     getUser(){
        this.axios.get('/user').then(()=>{
          //to-do保存到vuex里面
        })
     },
     getCartCount(){
         this.axios.get('/carts/products/sum').then(()=>{
          //to-do保存到vuex里面
        })
     }
   }
}
</script>

<style  lang="scss">
@import './assets/scss/reset.scss';
@import './assets/scss/config.scss';
@import './assets/scss/button.scss';

</style>
