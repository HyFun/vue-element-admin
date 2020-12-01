<template>
  <div class="app-container">
    <el-form>
      <el-form-item label="change事件触发">
        <el-select v-model="value" placeholder="请选择" @change="onChangeSelect">
          <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          />
        </el-select>
      </el-form-item>

      <el-form-item label="点击item事件触发">
        <el-select v-model="value" placeholder="请选择">
          <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          >
            <div @click="clickItem(item.label)">{{ item.label }}</div>
          </el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="上传文件">
        <el-button @click="clickUpload">点我上传</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
import Bus from '@/components/Uploader/bus'
export default {
  data() {
    return {
      options: [{
        value: '选项1',
        label: '黄金糕'
      }, {
        value: '选项2',
        label: '双皮奶'
      }, {
        value: '选项3',
        label: '蚵仔煎'
      }, {
        value: '选项4',
        label: '龙须面'
      }, {
        value: '选项5',
        label: '北京烤鸭'
      }],
      value: ''
    }
  },
  mounted() {
    // 文件选择后的回调
    Bus.$on('fileAdded', () => {
      console.log('文件已选择')
    })
    // 文件上传成功的回调
    Bus.$on('fileSuccess', () => {
      console.log('文件上传成功')
    })
  },
  destroyed() {
    Bus.$off('fileAdded')
    Bus.$off('fileSuccess')
  },
  methods: {
    onChangeSelect(event) {
      alert(event)
    },
    clickItem(name) {
      alert('点击了' + name)
    },
    clickUpload() {
      // 打开文件选择框
      Bus.$emit('openUploader', {
        id: '1111' // 传入的参数
      })
    }
  }
}
</script>
