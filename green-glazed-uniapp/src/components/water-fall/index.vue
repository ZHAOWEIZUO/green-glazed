<template>
  <view class="water-fall">
    <view class="column" v-for="(item, index) in computedList" :key="index">
      <view class="cell" v-for="(ite, inx) in item" :key="inx">
        <image mode="scaleToFill" @load="onImageLoad" class="image" :src="ite"></image>
        <text class="title">SK-II Skin Power大红瓶面霜滋润型50g 随机赠送小样</text>
        <view class="tip">
          <wd-tag
            custom-style="margin-right: 16rpx"
            custom-class="space"
            color="#369FE4"
            bg-color="#E6F2FA"
          >
            澳洲版
          </wd-tag>
          <wd-tag custom-class="tip-item" color="#369FE4" bg-color="#E6F2FA">澳洲直邮</wd-tag>
        </view>
        <view class="prise">
          <wd-tag
            custom-style="padding: 10rpx;"
            custom-class="prise-call"
            color="#F64741"
            bg-color="#FAE5DA"
          >
            <view class="member">会员券后价405</view>
            <view class="no-member">券后价410</view>
          </wd-tag>
        </view>
        <wd-text color="#666666" size="20rpx" text="￥410"></wd-text>
      </view>
    </view>
  </view>
</template>

<script lang="ts" setup>
// 接收传来的list
const { list, column, columnSpace } = defineProps(['list', 'column', 'columnSpace'])
console.log(list, column)
const DataList = ref({})
onMounted(() => {
  console.log('打印')
  initDate()
})

const computedList = ref([])
// 数据初始化
const initDate = () => {
  // 数据的分组
  const listNumber = Math.ceil(list.length / column)
  for (let index = 0; index < listNumber; index++) {
    computedList.value.push([])
  }
  let num = 0
  let initIndex = 0
  for (let index = 0; index < list.length; index++) {
    const element = list[index]
    computedList.value[initIndex].push(element)
    console.log(element)
    num = num + 1
    if (num === column) {
      initIndex = initIndex + 1
      console.log('换下个数组')
      num = 0
    }
  }
}

// const firstSectionHeight = computed(() => {
//   return async (item) => {
//     // let height
//     const imageInfoObj = await uni.getImageInfo({
//       src: item,
//     })
//     console.log(imageInfoObj.height)

//     return `${imageInfoObj.height}px`
//   }
// })

//  success: (res) => {
//   // imgLoad.value.imageWidth = res.width
//   height = res.height
//   console.log('图片高度', height)

//   // console.log('图片宽度:', imgLoad.value.imageWidth)
//   // console.log('图片高度:', imgLoad.value.imageHeight)
// },

const imgLoad = ref({
  imageSrc: '/static/images/scenery1.jpg',
  imageWidth: 0,
  imageHeight: 0,
})
const onImageLoad = (event) => {
  console.log(event)
}
</script>

<style>
.water-fall {
  width: 93%;
  /* height: 500rpx; */
  margin: 0 auto;
}
.column {
  display: flex;
  justify-content: space-between;
  margin-top: 10rpx;
}

.cell {
  width: 340rpx;
}

.image {
  width: 340rpx;
  height: 400rpx;
}

.title {
  font-family: 400;
  font-size: 24rpx;
}

:deep(.space) {
  width: 72rpx !important;
  height: 28rpx !important;
}

.prise {
  margin-top: 5rpx;
}

:deep(.prise-call) {
  padding: 5rpx;
}

.member {
  font-size: 20rpx;
  color: #f64741;
}

.no-member {
  font-size: 20rpx;
  color: #ef8c67;
}
</style>
