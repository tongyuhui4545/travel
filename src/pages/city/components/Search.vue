<template>
  <div class="search">
    <div class="search">
      <input type="text" class="search-input" placeholder="输入城市名或拼音" v-model="keyword">
    </div>
    <div v-show="keyword" class="search-content" ref="search">
      <ul>
        <li class="search-item border-bottom" v-for="item in list" :key="item.id" @click="handleCityChange(item.name)">{{
          item.name }}</li>
        <li class="search-item" v-show="list.length === 0">没有找到相关城市</li>
      </ul>
    </div>
  </div>
</template>

<script>
import Bscroll from 'better-scroll'
import { mapMutations } from 'vuex'
export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  data () {
    return {
      keyword: '',
      list: [],
      timer: null,
      scroll: null
    }
  },
  methods: {
    handleCityChange (city) {
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },
  mounted () {
    let bscrollDom = this.$refs.search
    this.scroll = new Bscroll(bscrollDom, { click: true })
  },
  watch: {
    keyword (val) {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      if (!this.keyword) {
        this.list = []
        return
      }
      this.timer = setTimeout(() => {
        let result = []
        for (let i in this.cities) {
          this.cities[i].forEach((city) => {
            if (city.spell.indexOf(this.keyword) > -1 || city.name.indexOf(this.keyword) > -1) {
              result.push(city)
            }
          })
        }
        this.list = result
      }, 100)
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/variables'
  .search
    height: .72rem
    background: $bgColor
    padding: 0 .1rem
    .search-input
      box-sizing: border-box
      width: 100%
      height: .62rem
      line-height: .62rem
      text-align: center
      border-radius: .06rem
      padding: 0 .1rem
  .search-content
    z-index: 1
    overflow: hidden
    position: absolute
    top: 1.58rem
    left: 0
    right: 0
    bottom: 0
    background: #eee
    .search-item
      line-height: .62rem
      padding-left: .2rem
      background: #fff
      color: #666
</style>
