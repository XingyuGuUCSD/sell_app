<template>
  <div id="app">
    <img src="./assets/logo.png">
    使用组件
    <HelloWorld/>
    <Test/>
  </div>
</template>

<script>
//导入组件
import HelloWorld from './components/HelloWorld'
import Test from './components/Test'

export default {
  name: 'App',
  components: {
  //注册组件
    HelloWorld,
    Test
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
