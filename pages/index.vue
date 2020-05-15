<template>
  <div>
    <h2>商品列表</h2>
    <ul>
      <li v-for="good in goods" :key="good.id">
        <nuxt-link :to="{name: 'index-id', params: { id: good.id }}">
          <span>{{ good.text }}</span>
          <span>￥{{ good.price }}</span>
          <button @click.prevent="addCart(good)">
            加购物车
          </button>
        </nuxt-link>
      </li>
    </ul>
    路由视图
    <nuxt-child />
  </div>
</template>
<script>
export default {
  async asyncData ({ $axios, error }) {
    // 运行是在组件创建前,this不可用
    // nuxt会传递上下文进来
    const { ok, goods } = await $axios.$get('/api/goods')
    if (ok) {
      // 返回数据会和data中的数据合并
      return { goods }
    }
    // 重定向
    error({ statusCode: 400, message: '数据查询失败' })
  },
  data () {
    return {
      goods: [
        // { id: 1, text: 'This is A class', price: 8999 },
        // { id: 2, text: 'This is B class', price: 8999 }
      ]
    }
  },
  methods: {
    addCart () {}
  },
  head () {
    return {
      title: 'class-list',
      meta: [{ name: 'description', hid: 'description', content: 'set page meta' }],
      link: [{ rel: 'favicon', href: 'favicon.ico' }]
    }
  }
}
</script>
