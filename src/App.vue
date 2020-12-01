<template>
  <div id="app">
    <router-view />
    <!-- 将上传组件全局注册 -->
    <global-uploader />
  </div>
</template>

<script>
import globalUploader from '@/components/Uploader/GlobalUploader'
export default {
  name: 'App',
  components: {
    globalUploader
  }
}
</script>
