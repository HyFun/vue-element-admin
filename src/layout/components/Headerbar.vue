<!--
* @Description:
* @Author: heyongfeng
* @Date: 2020-08-07
* @LastEditTime: 2020-08-07
* @LastEditors: heyongfeng
-->
<template>
  <div ref="header" class="header">
    <router-link :to="{path:'/'}">
      <h1>
        <img src="../../assets/images/logo.png" alt="云从科技 星罗AI工厂">
        <span>云从科技 星罗AI工厂</span>
      </h1>
    </router-link>
    <!-- 中间自由区域 -->
    <div class="header-middle" />
    <!-- 用户头像区域 -->

    <el-dropdown trigger="click">
      <div class="header-user el-dropdown-link">
        <img
          src="https://user-gold-cdn.xitu.io/2020/7/28/17395a8a2bf6c9e7?imageView2/1/w/180/h/180/q/85/format/webp/interlace/1"
          alt="用户头像"
        >
        <span>administrator</span>
        <!-- <i class="el-icon-arrow-down el-icon--right" /> -->
        <span class="el-icon-caret-bottom" style="margin-left:5px;" />
      </div>
      <el-dropdown-menu slot="dropdown">
        <el-dropdown-item>
          <span style="display: block;">修改密码</span>
        </el-dropdown-item>
        <el-dropdown-item divided>
          <span style="display: block;" @click="clickExitApp">退出登录</span>
        </el-dropdown-item>
      </el-dropdown-menu>
    </el-dropdown>
  </div>
</template>

<script>
// 导入引用js

// 导入组件

export default {
  components: {},
  data() {
    // 这里存放数据
    return {}
  },
  // 监听属性 类似于data概念
  computed: {},
  // 监控data中的数据变化
  watch: {},
  // 生命周期 - 挂载完成（可以访问DO元素）
  mounted() {
    // 更新store中的header的高度
    const headerbarHeight = this.$refs['header'].getBoundingClientRect().height
    this.$store.dispatch('settings/changeSetting', {
      key: 'headerbarHeight',
      value: headerbarHeight
    })
  },
  // 方法集合
  methods: {
    /**
     * 点击退出app按钮的点击事件
     */
    clickExitApp() {
      this.$confirm('确定退出当前用户？', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        this.$message({
          type: 'success',
          message: '退出成功'
        })
      }).catch(() => {
      })
    }
  }
}
</script>
<style lang='scss' scoped>
.header {
  position: relative;
  background-color: #2a2c44;
  height: 80px;
  padding: 0 30px 0 10px;
  color: #fff;
  display: flex;
  align-items: center;
  h1 {
    position: relative;
    display: inline-block;
    padding: 0;
    margin: 0;
    img {
      width: 320px;
      vertical-align: middle;
    }
    span {
      display: inline-block;
      width: 0;
      height: 0;
      overflow: hidden;
    }
  }

  .header-middle {
    flex: 1;
  }

  .header-user {
    cursor: pointer;
    height: 80px;
    line-height: 80px;
    img {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      transition: all 1s;
      vertical-align: middle;
      margin-right: 10px;
    }
    &:hover img {
      transform: rotate(360deg);
    }
    span {
      font-size: 18px;
      color: #fff;
      vertical-align: middle;
    }
  }
}
</style>
