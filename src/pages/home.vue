<template lang="html">
  <div class="container">
    <!-- 引入home-header 组件 -->
    <HomeHeader></HomeHeader>
    <div class="content">
      <ul class="cont-ul">
        <!-- 引入商品列表组件 -->
        <GoodList v-for="item in items" :price="item.price" :title="item.title" :img="item.img"></GoodList>
      </ul>
    </div>
    <!-- 引入底部展示组件 -->
    <CommonFooter></CommonFooter>
  </div>
</template>

<script >
  import HomeHeader from '../components/HomeHeader'
  import GoodList from '../components/GoodList'
  import CommonFooter from '../components/CommonFooter'

  export default {
    name: "home",
    data() {
      return {
        // 定义一个空数组items
        items: []
      }
    },
    // 局部注册组件，key和value名称相同，缩写如下
    components: {
      HomeHeader,
      GoodList,
      CommonFooter
    },
    created () {
      // 使用vue-resource来发送ajax请求数据
      this.$http.get('api/goods')
          .then((data) => {
            this.items = data.body.data;
          })
    }
  }
</script>

<style lang="css" scoped>
  .container {
    width: 100%;
    margin: 0 auto;
  }
  .content {
    margin-bottom: 1.8rem;
  }
  .cont-ul {
    padding-top: 0.5rem;
    background-color: #ccc;
  }
  .cont-ul::after {
    content: '';
    display: block;
    clear: both;
    width: 0;
    height: 0;
  }
</style>
