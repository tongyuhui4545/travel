<template>
  <div class="list" ref="wrapper">
    <div>
      <div class="area">
        <div class="title border-topbottom">当前城市</div>
        <div class="button-list">
          <div class="button-wrapper">
            <div class="button">{{ this.currentCity }}</div>
          </div>
        </div>
      </div>
      <div class="area">
        <div class="title border-topbottom">热门城市</div>
        <div class="button-list">
          <div class="button-wrapper" v-for="item of hot" :key="item.id">
            <div class="button" @click="handleCityChange(item.name)">{{ item.name }}</div>
          </div>
        </div>
      </div>
      <div class="area" v-for="(item, key) in cities" :key="key" :ref="key">
        <div class="title border-topbottom">{{ key }}</div>
        <div class="item-list">
          <div class="item border-bottom" v-for="innerItem of item" :key="innerItem.id"
            @click="handleCityChange(innerItem.name)">
            {{ innerItem.name }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Bscroll from 'better-scroll'
import { mapState, mapMutations } from 'vuex'
export default {
  name: 'CityList',
  computed: {
    ...mapState({
      currentCity: 'city'
    })
  },
  props: {
    hot: Array,
    cities: Object,
    letter: String
  },
  methods: {
    handleCityChange (city) {
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },
  mounted () {
    this.$nextTick(() => {
      let bscrollDom = this.$refs.wrapper
      this.scroll = new Bscroll(bscrollDom, { mouseWheel: true, click: true, tap: true })
    })
  },
  watch: {
    letter (val) {
      if (this.letter) {
        const element = this.$refs[this.letter][0]
        this.scroll.scrollToElement(element)
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/variables.styl'
  .border-topbottom
    &:before
      border-color: #ccc
    &:after
      border-color: #ccc
  .title
    line-height: .54rem
    background: #eee
    padding-left: .2rem
    color: #666
    font-size: .26rem
  .list
    overflow: hidden
    position: absolute
    top: 1.58rem
    bottom: 0
    left: 0
    right: 0
  .button-list
    padding: .1rem .6rem .1rem .1rem
    overflow: hidden
    .button-wrapper
      float: left
      width: 33.33%
      .button
        margin: .1rem
        padding: .1rem 0
        text-align: center
        border: .02rem solid #ccc
        border-radius: .06rem
  .item-list
    .item
      line-height: .74rem
      padding-left: .2rem
    .border-bottom
    &:before
      border-color: #ccc
</style>
