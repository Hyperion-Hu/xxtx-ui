<!--
 * @Author: your name
 * @Date: 2021-07-13 09:20:44
 * @LastEditTime: 2021-07-13 10:09:17
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \xxtx-ui\src\components\Head.vue
-->
<template>
  <div class="header">
    <div class="wrapper">
      <div class="logo">
        <img src="/images/logo.jpg" alt="" />
      </div>
      <div class="title" @click="toIndex">{{name}}</div>
      <ul class="category" v-for="item in categories" :key="item.id" @click="toList(item.id)">
        <li>{{ item.name }}</li>
      </ul>
      <div class="contact">
        <i>phone</i>
        <a href="#">联系我们</a>
      </div>
    </div>
  </div>
</template>
<script>
import { get } from '../../utils/request';
export default {
  data() {
    return {
      // 1. 声明变量
      categories: [],
      name: '行学天下',
    };
  },
  methods: {
    // 跳转回首页
    toIndex() {
      this.$router.push({
        path: '/',
      });
    },
    // 跳转到列表页面
    toList(categoryId) {
      this.$router.push({
        path: '/List',
        query: { categoryId },
      });
    },
    // 2. 加载栏目数据
    loadCategories() {
      let url = '/index/category/findAll';
      get(url).then(resp => {
        this.categories = resp.data;
      });
    },
    // 加载网站标题
    loadWebName() {
      let url = '/index/findByKey';
      get(url, {name: 'name'}).then(resp => {
        if(resp.data) {
          this.name = resp.data.val;
        }
      });
    },
  },
  created() {
    this.loadCategories();
    this.loadWebName();
  },
}
</script>
<style scoped>
/* 头部 */
.header {
  padding: 0.5em 0;
  box-shadow: 0 1px 5px #ccc;
}
.wrapper {
  width: 90%;
  margin: 0 auto;
}
.header .wrapper::after {
  content: "";
  display: block;
  clear: both;
}
.header .wrapper > * {
  float: left;
  height: 60px;
  line-height: 60px;
}
.header .logo {
  width: 60px;
  overflow: hidden;
}
.header .logo img {
  width: 100%;
}
.header .title {
  font-weight: bold;
  font-size: 20px;
  padding: 0 1em;
  cursor: pointer;
}
.header ul.category::after {
  content: "";
  display: block;
  clear: both;
}
.header ul.category > li {
  float: left;
  width: 80px;
  text-align: center;
  cursor: pointer;
}
.header .contact {
  float: right;
}
</style>