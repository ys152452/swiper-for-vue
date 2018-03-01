<template>
  <div class="swiper-group" :class='option.align + " " + option.direction' :style="swiperGroupStyle" >
      <slot></slot>
  </div>
</template>

<script>
export default {
  data () {
    return {
      swiperGroupStyle: {},
      option: {},
      optionInit: {
        height: '100%',
        width: '100%',
        direction: 'horizontal',
        align: 'around'
      }
    }
  },
  props: {
    propOption: {
      type: Object,
      default: {},
      required: true
    }
  },
  created () {
    this.option = Object.assign(this.optionInit, this.propOption)
    this.swiperGroupStyle = {
      height: this.option.height,
      width: this.option.width
    }
  },
  methods: {
    getWatcher (n) {
      const _this = this
      _this.$children.forEach(item => {
        item.swiperObj[item.propOption.propId].slideTo(n)
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "../../static/swiper.min.css";
.swiper-group {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
}
.swiper-group #swipeBoxLink {
    margin-top: 0;
}
.swiper-group.horizontal {
    flex-direction: row;
}
.swiper-group.vertical {
    flex-direction: column;
}
.swiper-group.around {
    justify-content: space-around;
}
.swiper-group.between {
    justify-content: space-between;
}
.swiper-group.horizontal .swiper-container {
    width: 45%;
    height: 100%;
}
.swiper-group.vertical .swiper-container {
    width: 100%;
    height: 45%;
}
</style>
