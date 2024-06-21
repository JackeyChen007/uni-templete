<!-- 使用 type="home" 属性设置首页，其他页面不需要设置，默认为page；推荐使用json5，更强大，且允许注释 -->
<route lang="json5" type="home">
{
  style: {
    navigationStyle: 'custom',
    navigationBarTitleText: '首页',
  },
}
</route>
<template>
  <view
    class="bg-white overflow-hidden pt-2 px-4"
    :style="{ marginTop: safeAreaInsets?.top + 'px' }"
  >
    <view class="mt-12">
      <image src="/static/logo.svg" alt="" class="w-28 h-28 block mx-auto" />
    </view>
    <view class="text-center text-4xl main-title-color mt-4">unibest</view>
    <view class="text-center text-2xl mt-2 mb-8">最好用的 uniapp 开发模板</view>

    <view class="text-justify max-w-100 m-auto text-4 indent mb-2">{{ description }}</view>
    <view class="text-center mt-8">
      当前平台是：
      <text class="text-green-500">{{ PLATFORM.platform }}</text>
    </view>
    <view class="text-center mt-4">
      模板分支是：
      <text class="text-green-500">base</text>
    </view>
  </view>
  <view class="p16 w-20 center m-auto">
    <up-button type="primary" text="确定"></up-button>
  </view>
  <view>
    <up-toast ref="uToastRef"></up-toast>
    <up-cell-group title-bg-color="rgb(243, 244, 246)">
      <up-cell
        :titleStyle="{ fontWeight: 500 }"
        :title="item.title"
        v-for="(item, index) in list"
        :key="index"
        isLink
        :icon="item.iconUrl"
        @click="showToast(item)"
      ></up-cell>
    </up-cell-group>
  </view>
  <view>
    <up-toast ref="uToastRef"></up-toast>
    <up-cell-group title-bg-color="rgb(243, 244, 246)">
      <up-cell
        :titleStyle="{ fontWeight: 500 }"
        :title="item.title"
        v-for="(item, index) in list"
        :key="index"
        isLink
        :icon="item.iconUrl"
        @click="showToast(item)"
      ></up-cell>
    </up-cell-group>
  </view>
</template>

<script lang="ts" setup>
import PLATFORM from '@/utils/platform'

defineOptions({
  name: 'Home',
})

// 获取屏幕边界到安全区域距离
const { safeAreaInsets } = uni.getSystemInfoSync()
const description = ref(
  'unibest 是一个集成了多种工具和技术的 uniapp 开发模板，由 uniapp + Vue3 + Ts + Vite4 + UnoCss + UniUI + VSCode 构建，模板具有代码提示、自动格式化、统一配置、代码片段等功能，并内置了许多常用的基本组件和基本功能，让你编写 uniapp 拥有 best 体验。',
)

onLoad(() => {})
const show = ref(false)
const list = ref([
  {
    type: 'default',
    title: '默认主题',
    message: '锦瑟无端五十弦',
    iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/default.png',
  },
  {
    type: 'error',
    icon: false,
    title: '失败主题',
    message: '一弦一柱思华年',
    iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png',
  },
  {
    type: 'success',
    title: '成功主题(带图标)',
    message: '庄生晓梦迷蝴蝶',
    iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/success.png',
  },
  {
    type: 'loading',
    title: '正在加载',
    message: '正在加载',
    iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/loading.png',
  },
  {
    type: 'default',
    title: '结束后跳转标签页',
    message: '此情可待成追忆',
    url: '/pages/componentsB/tag/tag',
    iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/jump.png',
  },
])

// 计算属性
const getIcon = computed(() => {
  return (path) => {
    return 'https://cdn.uviewui.com/uview/example/' + path + '.png'
  }
})
// 方法
const uToastRef = ref(null)
function showToast(params) {
  uToastRef.value.show({
    ...params,
    complete() {
      params.url &&
        uni.navigateTo({
          url: params.url,
        })
    },
  })
}
</script>

<style lang="scss">
.main-title-color {
  color: #d14328;
}
</style>
