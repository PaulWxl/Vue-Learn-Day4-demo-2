<template>
  <div class="app-container">
    <h1>App 根组件 --- {{ countFromSon }} </h1>

    <hr>
    
    <div class="box">
        <!-- 用 v-bind 向 子组件的 自定义属性 传递数据， 达到 父向子传值 -->
        <!-- 这是 父向子传值 的 关键步骤  -->
        <!-- msg/user 是 子组件 中 的 自定义 属性  -->
        <Left :msg="message" :user="userinfo"></Left>
        <Right @child-component-numChange="getNumberFromSon"></Right>
      </div>
    
  </div>
</template>

<script>

// 导入 子组件 
import Left from '@/components/Left.vue'
import Right from '@/components/Right.vue'


export default {

    // 注册 子组件 
    components: {
        Left,
        Right
    },
    data() {
       return {
          message:'hello 父向子传值',
          userinfo: {
            username: '魏小磊',
            id: '200540037'
          },
          // 先定义一个数据， 用来 接受 子组件 的 值, 并 初始化 为0 
          countFromSon: 0

       }
    },
    methods: {
      // 处理 自定义事件类型 的 程序
       getNumberFromSon(val) {
          this.countFromSon = val
       }

    }

}
</script>

<style lang="less" >
.app-container {
  padding: 1px 20px 20px;
  background-color: #efefef;
}
.box {
  display: flex;
}
</style>
