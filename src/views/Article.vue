<!--
 * @Description: 
 * @Author: charles
 * @Date: 2021-07-01 11:24:08
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2021-07-12 14:42:20
-->
<template>
  <div>
    <p class="title" @click="clickHandler">{{name}}</p>
  </div>
</template>
<style scoped>
  p.title {
    color: lightblue;
    font-size: 20px;
  }
</style>
<script>
export default {
  data() {
    return {
      name: '文章页面',
    };
  },
  methods: {
    clickHandler() {
      alert(this.name);
    },
  },
};
</script>