<template>
  <div>
    <el-header>
      <my-header />
    </el-header>
    <nuxt />
  </div>
</template>

<script>
  import MyHeader from '@/components/public/header'

  export default {
    components: { MyHeader }
  }
</script>
