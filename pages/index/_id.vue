<template>
  <div>
    detail:
    <pre>{{ goodInfo }}</pre>
  </div>
</template>

<script>
export default {
  name: 'Index',
  async asyncData ({ $axios, error, params }) {
    // 运行是在组件创建前,this不可用
    // nuxt会传递上下文进来
    if (params.id) {
      const { data: goodInfo } = await $axios.$get('/api/detail', { params })
      if (goodInfo) {
        // 返回数据会和data中的数据合并
        return { goodInfo }
      }
      // 重定向
      error({ statusCode: 400, message: '数据查询失败' })
    } else {
      return { goodInfo: null }
    }
  }
}
</script>

<style scoped>

</style>
