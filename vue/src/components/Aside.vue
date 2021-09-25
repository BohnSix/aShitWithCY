<template>
  <div>
    <el-menu
        style="width: 200px;min-height: calc(100vh - 50px)"
        default-active="2"
        class="el-menu-vertical-demo"    >
      <el-sub-menu index="1">
        <template #title>
          <i class="el-icon-location"></i>
          <span>系统管理</span>
        </template>
        <el-sub-menu index="1-4">
          <template #title>用户管理</template>
          <el-menu-item index="1-4-1">选项1</el-menu-item>
        </el-sub-menu>
      </el-sub-menu>

      <el-menu-item index="4">
        <i class="el-icon-setting"></i>
        <template #title>数据管理</template>
      </el-menu-item>
    </el-menu>
  </div>
</template>

<script>
export default {
  name: "Aside"
}
</script>

<style scoped>

</style>