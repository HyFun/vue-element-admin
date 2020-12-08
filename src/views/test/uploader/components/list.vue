<template>
  <div class="file_list">
    <div v-for="item in fileList" :key="item.uid">
      <div class="file_item">
        <a>
          <i class="icon el-icon-document" />
          {{ item.name }}
        </a>
        <div class="file_progress">
          <div>
            <span v-if="item.error" class="file_progress_error">上传失败</span>
            <span v-if="item._progress===0" class="file_progress_wait">等待上传</span>
            <el-progress v-if="item._progress>0 && item._progress<100" :percentage="item._progress" />
          </div>
        </div>
        <div class="file_oper">
          <i v-if="!item.error && item.completed || typeof item.cancel!=='function'" class="el-icon-upload-success el-icon-circle-check" />
          <i class="el-icon-close" @click="clickReove(item)" />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
// import File from './file'
export default {
  components: {
    // File
  },
  props: {
    fileList: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    /**
     * 点击移除文件
     */
    clickReove(file) {
      if (typeof file.cancel === 'function') {
        file.cancel()
      } else {
        // 从文件列表中移除
        const index = this.fileList.findIndex(v => v.uid === file.uid)
        if (index !== -1) {
          this.fileList.splice(index, 1)
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.file_list {
  margin-top: 10px;
}

.file_item {
  display: flex;
  align-items: center;
  font-size: 14px;
  padding: 5px 5px;
  margin-bottom: 5px;
  cursor: pointer;
  &:hover{
    background-color: #F5F7FA;
    a{
      color: #1890ff;
    }
    .el-icon-upload-success {
      display: none;
    }
    .file_oper .el-icon-close {
      display: block;
    }
  }
  a {
    .icon {
      color: #909399;
    }
    color: #606266;
  }

  .file_progress {
    flex: 1;
    padding: 0 20px;
    .file_progress_error {
      color: #e64340;
    }
  }

  .file_oper {
    width: 14px;
    height: 14px;
    position: relative;
    overflow: hidden;
    .el-icon-upload-success {
      color: #13ce66;
      position: absolute;
      right: 0;
      top: 0;
    }
    .el-icon-close {
      color: #606266;
      opacity: 0.75;
      display: none;
    }
  }
}
</style>
