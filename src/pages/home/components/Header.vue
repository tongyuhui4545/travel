<template>
  <div class="header">
    <div class="header-left">
      <div class="iconfont back-icon">&#xe624;</div>
    </div>
    <div class="header-input">
      <span class="iconfont">&#xe632;</span>
      输入城市
    </div>
    <router-link to='/city'>
      <div class="header-right arror-icon">
        {{ this.city }}
        <span class="iconfont">&#xe688;</span>
      </div>
    </router-link>
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  name: 'HomeHeader',
  computed: {
    ...mapState(['city'])
  }
}
</script>
<style lang="stylus" scoped>
@import '~styles/variables.styl'
  .header
    display: flex
    line-height: .86rem
    background: $bgColor
    color: #fff
    .header-left
      width: .64rem
      float: left
      .back-icon
        text-align:center
        font-size: .4rem
    .header-input
      flex: 1
      height: .64rem
      line-height: .64rem
      margin-left: .2rem
      margin-top: .12rem
      padding-left: .2rem
      background: #fff
      color: #ccc
      border-radius: .1rem
    .header-right
      min-width: 1.04rem
      padding: 0 .1rem
      float: right
      text-align: center
      .arrow-icon
        font-size: .24rem
        margin-left: -.04rem
</style>
