<template>
  <div>
    <el-upload
      action="string"
      :file-list="fileList"
      :auto-upload="true"
      :multiple="false"
      :limit="limit"
      :show-file-list="false"
      :before-upload="onBeforeUpload"
      :on-exceed="onExceed"
      :http-request="onHttpRequest"
      :on-change="onChange"
      :on-remove="onRemove"
    >
      <el-button ref="btn" type="primary" :loading="false">选择文件</el-button>
    </el-upload>
    <!-- 自定义的filelist -->
    <FileList v-if="fileList.length>0" :file-list="fileList" />
  </div>
</template>
<script>
import Uploader from 'simple-uploader.js'
import FileList from './list'
export default {
  components: {
    FileList
  },
  props: {
    options: {
      type: Object,
      default: () => {}
    },
    fileList: {
      type: Array,
      default: () => []
    },
    interceptorInit: {
      type: Function,
      default: (file, opt) => {}
    },
    interceptorSuccess: {
      type: Function,
      default: (file, response, opt) => {}
    },
    // 上传附件的最大数量
    limit: {
      type: Number,
      default: 1
    },
    // 接收文件类型
    accept: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      uploader: undefined
    }
  },
  created() {
    const uploader = new Uploader(this.options)
    this.uploader = uploader
    // 监听
    uploader.on('fileProgress', this.onUploaderFileProgress)
    uploader.on('fileAdded', this.onUploaderFileAdded)
    uploader.on('fileRemoved', this.onUploaderFileRemoved)
    uploader.on('fileSuccess', this.onUploaderFileSuccess)
  },
  beforeDestroy() {
    // 取消监听
    this.uploader.off('fileProgress')
    this.uploader.off('fileAdded')
    this.uploader.off('fileRemoved')
    this.uploader.off('fileSuccess')
  },
  methods: {
    // -----------el-upload--------------
    onBeforeUpload(file) {
      console.log('文件上传之前:::', file)
      // 需要检测附件
      if (Array.isArray(this.accept)) {
        if (this.accept.length === 0) {
          return true
        } else {
          // 检测
          const access = this.checkFileAccept(file)
          if (access) {
            return true
          } else {
            this.$message.error('请选择指定格式的附件')
            return false
          }
        }
      }
      return true
    },
    onExceed() {
      this.$message.error(`当前最多上传${this.limit}个附件`)
    },
    onHttpRequest(params) {
      console.log('el-uploader开始上传:::', params)
      if (!this.uploader.isUploading()) {
        this.uploader.addFile(params.file)
        this.uploader.upload()
      } else {
        this.$message.error('当前任务结束后才能上传')
      }
    },
    onChange(file, fileList) {

    },
    onRemove(file, fileList) {

    },
    // -----------uploader--------------
    /**
     * 计算上传的进度
     */
    onUploaderFileProgress(rootFile, file, chunk) {
      this.$set(file, '_progress', parseInt(chunk.endByte / file.size * 100))
    },
    /**
     * 文件添加
     */
    onUploaderFileAdded(file, event) {
      this.$set(file, '_progress', 0)
      file.uniqueIdentifier = file.uid
      this.fileList.push(file)
      // 进行初始化 并设置query中的值
      if (this.interceptorInit && typeof this.interceptorInit === 'function') {
        this.interceptorInit(file, this.options)
      }
      return true
    },
    /**
     * 文件被移除
     */
    onUploaderFileRemoved(file) {
      const index = this.fileList.findIndex(v => v.uid === file.uid)
      if (index !== -1) {
        this.fileList.splice(index, 1)
      }
    },
    /**
     * 文件上传成功
     */
    onUploaderFileSuccess(rootFile, file, response, chunk) {
      console.log('onUploaderFileSuccess>>>>response', res)
      const res = JSON.parse(response)
      // 成功之后的操作
      console.log('onUploaderFileSuccess>>>>res', res)
      this.interceptorSuccess(file, res, this.options)
    },
    // -----------其他方法--------------
    checkFileAccept(file) {
      const name = file.name.toLowerCase()
      let isAccess = false
      this.accept.forEach(item => {
        const reg = new RegExp('(.' + item.toLowerCase() + ')$')
        console.log('检测>>>', reg, reg.test(name))
        isAccess = reg.test(name) || isAccess
      })
      return isAccess
    }
  }
}
</script>
