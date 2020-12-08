<template>
  <div class="app-container">
    自定义上传组件
    <Uploader :options="options" :file-list="fileList" />
  </div>
</template>
<script>
import Uploader from './components/index'
export default {
  components: {
    Uploader
  },
  data() {
    return {
      fileList: [{ name: '1234.txt' }],
      options: {
        target: '/mgt-api/v1/app/upload/client/chunk',
        chunkSize: '2048000',
        fileParameterName: 'file',
        maxChunkRetries: 1,
        testChunks: false,
        processParams: (params) => {
          // 处理请求参数
        //   return { ...this.options.query, partNumber: params.chunkNumber }
          if (this.options.chunkParams) {
            return { ...this.options.chunkParams, partNumber: params.chunkNumber }
          }
          return params
        },
        query: {}
      }
    }
  }
}
</script>
