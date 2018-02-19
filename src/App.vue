<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <Myheader :poiInfo='poiInfo'></Myheader>
    <Mynav></Mynav>

    <!-- <div class="nav">
      nav
    </div> -->

    <!-- <div class="content">
      content
    </div> -->
    <!-- <HelloWorld/>
    <Test/> -->

    <router-view></router-view>
    
  </div>
</template>

<script>

//导入组件
// import HelloWorld from './components/HelloWorld'
// import Test from './components/Test'
import Myheader from 'components/Header/Header'
import Mynav from 'components/Nav/Nav'

export default {
  name: 'App',
  components: {
  //注册组件
    // HelloWorld,
    // Test
    Myheader,
    Mynav
  },

  data(){
    return{
      //header组件需要的信息（商家信息）
      poiInfo:{}
    }
  },

  created(){//发起异步请求，获取数据

    var that = this;
    //通过axios发起get请求
      this.$axios.get('/api/goods')
            .then(function (response) {//获取到数据
              //console.log(response);
              var dataSource = response.data;
              console.log(dataSource);
              if(dataSource.code == 0){
                that.poiInfo = dataSource.data.poi_info;
                //console.log(that.poiInfo);
              }
            })
            .catch(function (error) {//出错数据
              console.log(error);
            });
    }
}
</script>

<style>
/*#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}*/
</style>
