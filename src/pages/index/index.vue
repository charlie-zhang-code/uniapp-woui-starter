<script setup lang="ts">
const searchType = ref<string>('全部')
const value = ref<string>('')
const menu = ref([
  {
    content: '全部',
  },
  {
    content: '订单号',
  },
  {
    content: '退款单号',
  },
])
function changeSearchType({ item, index }) {
  searchType.value = item.content
}

const swiperList = ref([
  'https://registry.npmmirror.com/wot-design-uni-assets/*/files/panda.jpg',
  'https://registry.npmmirror.com/wot-design-uni-assets/*/files/moon.jpg',
])
const current = ref<number>(0)

function handleClick(e) {
  // console.log(e)
}
function onChange(e) {
  // console.log(e)
}
const tab = ref<number>(0)
</script>

<template>
  <view>
    <wd-notice-bar closable text="这是一条消息提示信息，这是一条消息提示信息，这是一条消息提示信息" prefix="warn-bold" />

    <wd-search v-model="value" hide-cancel>
      <template #prefix>
        <wd-popover mode="menu" :content="menu" @menuclick="changeSearchType">
          <view class="search-type">
            <text>{{ searchType }}</text>
            <wd-icon custom-class="icon-arrow" name="fill-arrow-down" />
          </view>
        </wd-popover>
      </template>
    </wd-search>

    <wd-swiper
      v-model:current="current" class="mt-2" :list="swiperList" autoplay :indicator="{ type: 'dots-bar' }"
      @click="handleClick" @change="onChange"
    />

    <!-- #ifdef MP-WEIXIN -->
    <wd-tabs v-model="tab" :offset-top="80" :map-num="4" animated swipeable sticky>
      <block v-for="item in 8" :key="item">
        <wd-tab :title="`标签${item}`" class="p-x-2 p-y-1">
          <view v-for="index in 400" :key="index">
            <view>内容{{ index }}</view>
          </view>
        </wd-tab>
      </block>
    </wd-tabs>
    <!-- #endif -->

    <!-- #ifdef WEB -->
    <wd-tabs v-model="tab" :offset-top="0" :map-num="4" animated swipeable sticky>
      <block v-for="item in 8" :key="item">
        <wd-tab :title="`标签${item}`" class="p-x-2 p-y-1">
          <view v-for="index in 400" :key="index">
            <view>内容{{ index }}</view>
          </view>
        </wd-tab>
      </block>
    </wd-tabs>
    <!-- #endif -->
  </view>
</template>

<style scoped lang="scss">
  .search-type {
    position: relative;
    height: 30px;
    line-height: 30px;
    padding: 0 8px 0 16px;
  }

  .search-type::after {
    position: absolute;
    content: '';
    width: 1px;
    right: 0;
    top: 5px;
    bottom: 5px;
    background: rgba(0, 0, 0, 0.25);
  }

  .search-type {
    :deep(.icon-arrow) {
      display: inline-block;
      font-size: 20px;
      vertical-align: middle;
    }
  }
</style>

<route type="home" lang="json">
  {
  "layout": "default",
  "name": "index",
  "style": {
  "navigationBarTitleText": "首页"
  }
  }
</route>
