<template>
  <div class="step_container">
    <div
      v-for="(item, index) in steps"
      :key="index"
      class="step_item"
      :class="{ 'current': active === index,'actived': index<active}"
    >
      <el-tooltip
        class="item"
        effect="dark"
        :content="item.tips"
        placement="top"
      >
        <div class="step_item_content">
          <div class="step_item_circle">
            <span v-if="active <= index">{{ index + 1 }}</span>
            <i v-else class="el-icon-check" />
          </div>
          <div>{{ item.title }}</div>
        </div>
      </el-tooltip>
      <div v-if="index !== steps.length - 1" class="step_item_line" />
    </div>
  </div>
</template>
<script>
export default {
  props: {
    steps: {
      type: Array,
      default: () => []
    },
    active: {
      type: Number,
      default: 0
    }
  }
}
</script>
<style lang="scss" scoped>
.step_container {
  display: flex;
  .step_item {
    flex: 1;
    display: flex;
    align-items: center;
    &:last-child {
      flex: 0;
    }

    .step_item_content {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      white-space: nowrap;
      margin: 5px;
      cursor: pointer;
      color: #c0c4cc;
      .step_item_circle {
        width: 24px;
        height: 24px;
        border-radius: 50%;
        border: 2px solid #c0c4cc;
        text-align: center;
        line-height: 22px;
        margin-bottom: 5px;
      }
    }
    .step_item_line {
      flex: 1;
      width: 0;
      height: 2px;
      background-color: #c0c4cc;
    }
  }

  .step_item {
    &.current {
      .step_item_content {
        color: #333;
      }
      .step_item_circle {
        border-color: #333;
      }
      .step_item_line {
        // background-color: #333;
      }
    }
  }

    .step_item {
    &.actived {
      .step_item_content {
        color: #67c23a;
      }
      .step_item_circle {
        border-color: #67c23a;
      }
      .step_item_line {
        background-color: #67c23a;
      }
    }
  }
}
</style>
