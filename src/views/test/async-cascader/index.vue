<template>
  <div class="app-container">
    <el-form>
      <el-form-item label="正常情况：">
        <el-cascader
          v-model="form.normal"
          :options="cityList"
          :props="{ value: 'name', label: 'name' }"
          style="width: 100%"
          @change="onAddressChange"
        />
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
import cityList from './city'

export default {
  data() {
    return {
      cityList: cityList,
      form: {
        normal: []
      }
    }
  }
}
</script>
