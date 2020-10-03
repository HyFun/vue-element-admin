<template>
  <draggable :list="roleList" :group="roleType" @change="onDragChange">
    <el-tag v-for="(item, index) in roleList" :key="index" type="success">{{ item.name }}</el-tag>
  </draggable>
</template>
<script>
import draggable from 'vuedraggable'

export default {
  components: {
    draggable
  },
  props: {
    roleList: {
      required: true,
      type: Array,
      default: () => []
    },
    roleType: {
      required: true,
      type: String,
      default: ''
    },
    nodeId: {
      type: String,
      default: ''
    }
  },
  methods: {
    /**
     * 拖拽改变事件
     */
    onDragChange(event) {
      console.log('拖拽了>>>>', event)
    }
  }
}
</script>
<style lang="scss" scoped>
.el-tag {
  cursor: pointer;
  margin-right: 5px;
  margin-bottom: 5px;
}
</style>
