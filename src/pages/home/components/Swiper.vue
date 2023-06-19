<template>
  <div class="wrapper">
    <swiper :options="swiperOption">
      <swiper-slide
        v-for='itm in swiperList'
        :key="itm.id"
      >
        <img
          class="swiper-img"
          :src="itm.imgUrl"
        />
      </swiper-slide>
      <div
        class="swiper-pagination"
        slot="pagination"
      ></div>
    </swiper>

  </div>
</template>

<script>
import { swiper, swiperSlide } from 'vue-awesome-swiper'
export default {
  name: 'HomeSwiper',
  components: {
    swiper,
    swiperSlide
  },
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        loop: true
      },
      swiperList: [
        {
          id: '0001',
          imgUrl: require('@/assets/pics/goku1.jpg')
        },
        {
          id: '0002',
          imgUrl: require('@/assets/pics/goku2.jpg')
        }
      ]
    }
  }
}
</script>

<style lang="stylus">
.wrapper >>> .swiper-pagination-bullet-active {
  background: #fff !important;
}

.wrapper {
  overflow: hidden;
  width: 100%;
  height: 0;
  padding-bottom: 31.25%;
  background: #eee;
}

.swiper-img {
  width: 100%;
}
</style>
