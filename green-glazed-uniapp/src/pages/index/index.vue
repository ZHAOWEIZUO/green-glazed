<!-- 使用 type="home" 属性设置首页，其他页面不需要设置，默认为page；推荐使用json5，更强大，且允许注释 -->
<route lang="json5" type="home">
{
  style: {
    navigationStyle: 'custom',
    // navigationBarBackgroundColor: '#2baeff',
    // navigationBarTitleText: '首页',
    navigationBarTextStyle: 'white',
  },
}
</route>
<template>
  <!-- <view class="bg-white overflow-hidden" >  :style="{ paddingTop: safeAreaInsets?.top + 'px' }"-->
  <view class="container-header">
    <view class="container-top">
      <wd-navbar
        safeAreaInsetTop
        title="首页"
        custom-style="background-color: transparent !important; color: #fff !important"
        :bordered="false"
      ></wd-navbar>
      <wd-swiper
        class="container-swiper"
        :list="swiperList"
        autoplay
        v-model:current="current"
        custom-image-class="custom-image"
        height="260rpx"
      ></wd-swiper>
    </view>
  </view>
  <waterFall :list="swiperList" :column="2"></waterFall>
  <wd-loadmore custom-class="loadmore" state="finished" />
</template>

<script lang="ts" setup>
import PLATFORM from '@/utils/platform'
import waterFall from '@/components/water-fall/index.vue'

defineOptions({
  name: 'Home',
})

// 获取屏幕边界到安全区域距离
const { safeAreaInsets } = uni.getSystemInfoSync()

const waterFallList = ref([])

const current = ref<number>(0)

const swiperList = ref([
  'https://fastly.picsum.photos/id/866/200/300.jpg?hmac=rcadCENKh4rD6MAp6V_ma-AyWv641M4iiOpe1RyFHeI',
  'https://registry.npmmirror.com/wot-design-uni-assets/*/files/capybara.jpg',
  'https://registry.npmmirror.com/wot-design-uni-assets/*/files/panda.jpg',
  'https://registry.npmmirror.com/wot-design-uni-assets/*/files/moon.jpg',
  'https://registry.npmmirror.com/wot-design-uni-assets/*/files/meng.jpg',
])
</script>

<style>
.main-title-color {
  color: #d14328;
}

.container-header {
  height: 477rpx;
}
.container-top {
  width: 100%;
  height: 350rpx;
  background-color: rgba(43, 174, 255, 100%);
  border-radius: 0 0 50% 50%;
}

:deep(.wd-navbar__title) {
  color: #fff !important;
}

:deep(.wd-swiper) {
  width: 702rpx;
  height: 260rpx;
  margin: 0 auto;
  margin-top: 40rpx;
}
</style>
