<!--
 * @Description: 
 * @Author: charles
 * @Date: 2021-07-12 10:56:47
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2021-07-13 09:28:44
-->
<template>
  <!-- 容器 -->
  <div class="home">
    <!-- 头部 -->
    <Head/>
    <!-- /头部 -->

    <!-- 轮播 -->
    <div class="carousel">
      <el-carousel :interval="5000" arrow="always">
        <el-carousel-item v-for="item in carousels" :key="item.id">
          <img :src="item.url" alt="" style="width: 100%" />
        </el-carousel-item>
      </el-carousel>
    </div>
    <!-- /轮播 -->

    <!-- 项目列表 -->
    <div class="projects">
      <div class="wrapper">
        <!-- 项目 -->
        <div class="project" v-for="item in projects" :key="item.id">
          <div class="picture">
            <img :src="item.figure" alt="" />
          </div>
          <div class="info">
            <div class="title">{{item.name}}</div>
            <div class="time">{{item.beginTime | fmtDate}} ~ {{item.endTime | fmtDate}}</div>
            <div class="introduce">{{item.introduce}}</div>
          </div>
        </div>
        <!-- /项目 -->
      </div>
    </div>
    <!-- /项目列表 -->

    <!-- ... -->

    <!-- 底部 -->
    <!-- /底部 -->
  </div>
</template>

<script>
import { get } from "../utils/request";
import Head from './components/Head';
export default {
  components: { Head },
  data() {
    return {
      carousels: [],
      categories: [],
      projects:[],
    };
  },
  // 生命周期钩子 - Vue 实例刚刚创建完成，页面还没完全渲染出来的时候
  created() {
    this.loadCarousels();
    this.loadCategories();
    this.loadProjects();
  },
  methods: {
    loadProjects() {
      let url = '/index/project/pageQuery';
      get(url, {page: 1, pageSize: 3}).then(resp => {
        this.projects = resp.data.list;
      });
    },
    loadCategories() {
      let url = "/index/category/findAll";
      get(url).then(resp => {
        this.categories = resp.data;
      });
    },
    // 加载轮播图数据
    loadCarousels() {
      let url = "/index/carousel/findAll";
      get(url).then((resp) => {
        this.carousels = resp.data;
      });
    },
  },
};
</script>

<style scoped>
/* 产品 */
.projects {
  padding: 0.5em 0;
}
.projects .project {
  padding: 0.5em 0;
  border-bottom: 1px solid #ededed;
}
.projects .project > .picture {
  float: left;
  width: 400px;
  height: 300px;
  background-color: #ededed;
}
.projects .project > .picture img {
  width: 100%;
}
.projects .project > .info {
  margin-left: 420px;
  height: 300px;
}

/* 共用 */
.wrapper {
  width: 90%;
  margin: 0 auto;
}
</style>