<template>
<el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal" @select="handleSelect">
    <el-menu-item index="4"><n-link to="/category" prefetch>Category</n-link></el-menu-item>
</el-menu>
</template>

<script>
export default {
    name: "Navbar"
}
</script>