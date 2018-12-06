<template>
  <div id="app">
    <h2>1.侧边导航栏</h2>
    <ul class="slid-bar">
      <sliderbar :key="key" v-for="(item,key) in list" :item="item"></sliderbar>
    </ul>
    <h2>2.星星组件</h2>
    <star v-model="value"></star><span>可选择</span>
    <star v-model="value1" :disabled="true"></star><span>不可选择</span>
    <h2>3.分页组件</h2>
    <pagination :total="pagecount"></pagination>
    <router-view/>
  </div>
</template>

<script>
import sliderbar from "@/components/sliderbar";
import star from "@/components/star";
import pagination from "@/components/pagination";
export default {
  name: 'App',
  components:{
    sliderbar,star,pagination
  },
  data(){
    return {
      value:3,
      value1:2,
      list: [
          {
              text: '简介',
              link: '',
              level:'1'
          },
          {
              text: '快速入门',
              link: '',
              level:'1'
          },
          {
              text: '用户指南',
              list: [
                  {
                      text: '架构',
                      link: '',
                      level:2,
                      list:[
                        {
                          text: '三级菜单1',
                          link: '',
                          level:3
                        },
                        {
                          text: '三级菜单2',
                          link: '',
                          level:3
                        }
                      ]
                  },
                  {
                      text: '作业管理',
                      link: '',
                      level:2
                  },
                  {
                      text: 'weiclient',
                      link: '',
                      level:2
                  },
                  {
                      text: 'yarn批处理',
                      link: '',
                      level:2
                  },
                  {
                      text: 'k8s&tensorflow分布式',
                      link: '',
                      level:2
                  }
              ],
              level:'1'
          },
          {
              text: '最佳实践',
              list: [
                  {
                      text: '跨集群迁移数据',
                      link: '',
                      level:2
                  }
              ],
              level:'1'
          },
          {
              text: '常见问题',
              link: '',
              level:'1'
          },
          {
              text: '扩展阅读',
              link: '',
              level:'1'
          },
      ],
      pagecount:100
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  margin-left: 20px;
}
h2{
  margin-bottom: 20px;
  margin-top: 20px;
}
.slid-bar{
  margin-left: 50px;
  width: 400px;
  background-color: #f7f7f7;
  padding: 20px;
}
.slid-bar>li{
  width: 100%;
}
</style>
