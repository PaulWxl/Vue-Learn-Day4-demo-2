<template>
  <div class="left-container">
    <h3 >Left 组件</h3>

    <hr >
    <!-- 注意 插值表达式 中的 变量， 是自己的变量， （只不过是 自定义的 ）， 在 父组件 中 通过 v-bind 向 子组件 的  自定义属性 传递了 数据。  -->
    <!-- 插值表达式 中 是 子组件 自己的 定义的 属性  -->
    <p>message 的值：{{ msg }} </p>
    <p>username: {{ user.username }}</p>
    <p>userid: {{ user.id }}</p>

    <hr>

    <button @click="sendMsg">发送数据给Right.vue</button>


    <hr>

    <p> msgFromRight:  {{ msgFromRight }}</p>
  </div>

  
</template>

<script>
import bus from './eventBus'
export default {
  // 通过在 子组件 中 自定义 属性， 达到 父向子传值
  props: ['msg', 'user'],
  data() {
    return {
      str: '床前明月光，疑是地上霜',
      msgFromRight: ''
    }
  },
  methods: {
    sendMsg() {
      bus.$emit('share', this.str)
    },
    
  },
  created() {
    bus.$on('Right-Component-share', val => {
      this.msgFromRight = val
    })
  }
}
</script>

<style lang="less" scoped >
.left-container {
  padding: 0 20px 20px;
  background-color: orange;
  min-height: 250px;
  flex: 1;
  
}
// 这是CSS选择器的写法，用于选择具有特定属性的HTML元素。

// 在这个选择器中，h3表示选择对应的元素为h3标签（即HTML中的标题3），中括号[]内的data-v-001则表示要选择具有data-v-001属性的h3元素。

// 简单来说，在HTML文档中，所有具有data-v-001属性的h3元素都会受到这个CSS规则的影响，实现文本颜色为红色。
h3 {
  color: red;
}
/deep/  h5 {
  color: pink;
}

</style>
