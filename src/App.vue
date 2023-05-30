<template>
  <nav>
    <!-- <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link> -->
    <el-menu
    :default-active="activeIndex"
    class="el-menu-demo"
    mode="horizontal"
    :ellipsis="false"
    @select="handleSelect"
  >
    <el-menu-item index="0">
      <img src="./assets/logo.png" style="height: 40px;" >
    </el-menu-item>
    <div class="flex-grow" ></div>
    <el-menu-item index="1">
      <router-link to="/">服务历史</router-link>
    </el-menu-item>
    <el-menu-item index="2">
      <router-link to="/service">发起服务</router-link>
    </el-menu-item>
    <el-menu-item index="3">
      <router-link to="/profile">个人信息</router-link>
    </el-menu-item>
    <el-menu-item index="4">
      <router-link to="/about">关于我们</router-link>
    </el-menu-item>


  </el-menu>
  </nav>
  <router-view/>

</template>

<!-- ts -->
<script lang="ts" setup>
import { ref } from 'vue'

const activeIndex = ref('1')
const handleSelect = (key: string, keyPath: string[]) => {
  console.log(key, keyPath)
}
</script>

<!-- css -->
<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.flex-grow {
  flex-grow: 1;
}
.router-link-active {
    text-decoration: none;//去除默认样式
    color: orange;//高亮的颜色
  }
  a{
    text-decoration: none;
    color: grey;
  }
</style>


