<template>
  <div class="app-container">
    <Steps :steps="steps" :active="active" />
    <el-button @click="clickNext">下一步</el-button>
  </div>
</template>
<script>
// 组件
import Steps from './Steps'
export default {
  components: {
    Steps
  },
  data() {
    return {
      active: 0,
      steps: [
        {
          title: '步骤一',
          tips: '这是一段文字提示'
        },
        {
          title: '第二步',
          tips: '这是一段文字提示'
        },
        {
          title: '第三步',
          tips: '这是一段文字提示'
        }
      ]
    }
  },
  methods: {
    clickNext() {
      if (this.active < this.steps.length) {
        this.active++
      } else {
        this.active = 0
      }
    }
  }
}
</script>
