<template>
  <div class="right-container" >
    <h3 >Right 组件 --- {{ count }}</h3>
    <button @click="add">+1</button>
    <hr >
    <p>{{ msgFromLeft }}</p>
    <hr>
    <button @click="sendMsgToLeft">发送数据给Left.vue</button>
  </div>
</template>

<script>
import bus from './eventBus'
export default {
  data() {
    return {
      // 这是 子组件 自己 的 数据（count）， 将来 希望 把 count 值传给 父组件
      count: 0,
      str: '哈哈哈哈哈',
      // 定义一个 接收 数据 的 值： msgFromLeft 
      msgFromLeft: ''
    }
  },
  methods: {
    add() {
      this.count ++
      // 自定义事件类型名称通常是驼峰式命名的字符串，如 “customEvent”。

      // 在一些特定的场景中，事件类型名称可能具有特定的命名约定。例如，在Vue.js中，组件自定义事件的命名应该以子组件命名为前缀，使用短横线分隔单词，如 “child-component-click”。
      this.$emit('child-component-numChange', this.count)
    
    },
    sendMsgToLeft() {
      bus.$emit('Right-Component-share', this.str)
    }

  },
  created() {
    bus.$on('share', val => {
      this.msgFromLeft = val
    })
  }
}
</script>

<style lang="less" scoped>
.right-container {
  padding: 0 20px 20px;
  background-color: lightskyblue;
  min-height: 250px;
  flex: 1;
}
h3 {
  color: #6c99c5;
}

</style>
