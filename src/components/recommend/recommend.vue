<template>
  <div class="recommend">
    <div class="recommend-content">
      <div v-if="recommends.length" class="slider-wrapper">
        <slider>
          <div v-for="item in recommends">
            <a :href="item.linkUrl">
              <img class="needsclick" :src="item.picUrl" alt="">
            </a>
          </div>
        </slider>
      </div>
      <div class="recommend-list">
        <h1 class="list-title">热门歌单推荐</h1>
        <ul></ul>
      </div>
    </div>
  </div>
</template>
<script type="text/ecmascript-6">
  import Slider from 'base/slider/slider'
  import {getRecommend, getDistList} from 'api/recommend'
  import {ERR_OK} from 'api/config'
  export default {
    data() {
      return {
        recommends: []
      }
    },
    created() {
      this._getRecommend()
      this._getDistList()
    },
    methods: {
      _getRecommend() {
        getRecommend().then(res => {
          if (res.code === ERR_OK) {
            console.log(res.data.slider)
            this.recommends = res.data.slider
          }
        })
      },
      _getDistList() {
        getDistList().then(res => {
          if (res.code === ERR_OK) {
            console.log(res)
          }
        })
      }
    },
    components: {
      Slider
    }
  }
</script>
<style lang="stylus" scoped rel="stylesheet/stylus">
  @import "~common/stylus/variable"
  .recommend
    position: fixed
    width: 100%
    top: 5.5rem
    bottom: 0
    .recommend-content
      height: 100%
      overflow: hidden
      .slider-wrapper
        position: relative
        width: 100%
        overflow: hidden
      .recommend-list
        .list-title
          height: 65px
          line-height: 65px
          text-align: center
          font-size: $font-size-medium
          color: $color-theme
</style>
