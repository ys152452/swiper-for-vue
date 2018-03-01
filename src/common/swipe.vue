<template>
  <div :class="this.option.navigate.position === 'outside'?'swiper-container-out swiper-container ':'swiper-container ' + propOption.propId" :style="swiperStyle">
    <div :id="propOption.propId" class="swiper-container-box">
      <div class="swiper-wrapper">
        <div v-for="(item, key, index) in listData" :key='index' class="swiper-slide">
          <img class="swiper-slide-container" v-if='item.type==="img" && !loading' :src="item.src">
          <img class="swiper-slide-container swiper-lazy" v-if='item.type==="img" && loading' :data-src="item.src">
          <div class="swiper-lazy-preloader" v-if='loading'></div>
          <div class="swiper-slide-container swiper-slide-file" v-if='item.type==="txt"'>
            <img src='../assets/txt.png'>
            <p @click="checkFile(item.src, 'txt')">{{item.src.split('/')[item.src.split('/').length - 1]}}</p>
          </div>
          <div class="swiper-slide-container swiper-slide-file" v-if='item.type==="pdf"'>
            <img src='../assets/pdf.png'>
            <p @click="checkFile(item.src, 'pdf')">{{item.src.split('/')[item.src.split('/').length - 1]}}</p>
          </div>
          <div class="swiper-slide-container swiper-slide-file" v-if='item.type==="video"'>
            <img src='../assets/video.png'>
            <p @click="checkFile(item.src, 'video')">{{item.src.split('/')[item.src.split('/').length - 1]}}</p>
          </div>
          <div class="swiper-slide-container swiper-slide-file" v-if='item.type==="audio"'>
            <img src='../assets/audio.png'>
            <p @click="checkFile(item.src, 'audio')">{{item.src.split('/')[item.src.split('/').length - 1]}}</p>
          </div>
        </div>
      </div>
      <div :class="propOption.propId + '-modal file-show-box'" v-if="option.hasFile" @click="hideFile">
        <div class="file-box">
          <iFrame v-if='fileType === "pdf" || fileType === "txt"' autoPlay='true' :src="fileSrc"  width="100%" height="100%" border=1></iFrame>
          <audio width="100%" height="100%" :src="fileSrc" v-if='fileType === "audio"'>
            your browser does not support the audio tag
          </audio>
          <video width="100%" height="100%" autoplay :src="fileSrc" v-if='fileType === "video"' controls="controls">
            your browser does not support the video tag
          </video>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Swiper from '../../static/swiper.min.js'
export default {
  data () {
    return {
      swiperObj: {},
      swiperStyle: {},
      swiperPagination: {},
      navigation: {},
      loading: this.propOption.lazy,
      isObserver: this.propOption.observer,
      fileSrc: '',
      fileType: '',
      option: {},
      optionDefault: {
        hasFile: false,
        slidesPerView: 1,
        direction: 'horizontal',
        initialSlide: 0,
        speed: 300,
        effect: 'slide',
        coverflowEffect: {},
        preloadImages: true,
        loop: false,
        observer: false,
        autoplay: false,
        pagination: {},
        spaceBetween: 0,
        lazy: false,
        navigate: {
          position: 'inside',
          type: 'default'
        },
        uniqueNavElements: false,
        bulletsColor: '#007aff'
      }
    }
  },
  props: {
    'listData': {
      type: Array,
      default: []
    },
    'propOption': {
      type: Object,
      default: {}
    }
  },
  created () {
    this.option = Object.assign(this.optionDefault, this.propOption)
    if (this.$listeners.hasOwnProperty('last')) {
      this.isObserver = true
      this.loading = true
    }
    if (this.option.hasOwnProperty('navigate')) {
      if (this.option.navigate.position === 'outside') {
        this.option.uniqueNavElements = true
      }
      if (!this.option.navigate.hasOwnProperty('type')) {
        this.option.navigate['type'] = 'default'
      }
    }
    this.swiperStyle = {
      height: this.option.height,
      width: this.option.width
    }
    if (this.option.effect === 'coverflow') {
      this.option.coverflowEffect = {
        rotate: 50,
        stretch: 0,
        depth: 100,
        modifier: 1,
        slideShadows: true
      }
    }
  },
  mounted () {
    const _this = this
    new Promise((resolve, reject) => {
      if (_this.$parent.$options._componentTag !== 'c-swiper-group') {
        _this.$parent._data[_this.option.propId + 'Index'] = _this.option.initialSlide
      }
      if (Object.entries(_this.option.pagination).length > 0) {
        _this.ctrlNode('el', 'pagination', 'swiper-pagination-' + _this.option.propId)
      }
      if (_this.propOption.hasOwnProperty('navigate')) {
        _this.ctrlNode('prevEl', 'navigation', 'swiper-button-prev')
        _this.ctrlNode('nextEl', 'navigation', 'swiper-button-next')
      }
      resolve()
    }).then(() => {
      _this.swiperObj[_this.option.propId] = new Swiper('#' + _this.option.propId, {
        slidesPerView: _this.option.slidesPerView,
        direction: _this.option.direction,
        initialSlide: _this.option.initialSlide,
        speed: _this.option.speed,
        effect: _this.option.effect,
        coverflowEffect: _this.option.coverflowEffect,
        preloadImages: _this.option.preloadImages,
        loop: _this.option.loop,
        observer: _this.isObserver,
        autoplay: _this.option.autoplay,
        pagination: _this.option.pagination,
        navigation: _this.navigation,
        lazy: _this.loading,
        uniqueNavElements: _this.option.navOut,
        spaceBetween: _this.option.spaceBetween,
        grabCursor: true,
        setWrapperSize: true,
        on: {
          init: () => {
            _this.$nextTick(() => {
              if (Object.entries(_this.option.pagination).length > 0 && _this.option.pagination.type === 'bullets') {
                _this.swiperObj[_this.option.propId].pagination.bullets.css('background', _this.option.bulletsColor)
              }
            })
          },
          slideChange: () => {
            _this.$nextTick(() => {
              _this.$parent._data[_this.option.propId + 'Index'] = _this.swiperObj[_this.option.propId].activeIndex
              if (_this.$parent.$options._componentTag === 'c-swiper-group') {
                _this.$parent.getWatcher(_this.swiperObj[_this.option.propId].activeIndex)
              }
            })
          },
          slideChangeTransitionEnd: () => {
            _this.$nextTick(() => {
              _this.$parent._data[_this.option.propId + 'Index'] = _this.swiperObj[_this.option.propId].activeIndex
              if (_this.swiperObj[_this.option.propId].isEnd) {
                _this.$emit('last')
              }
            })
          },
          resize: () => {
            _this.throttle(_this.swiperResize, window)
          }
        }
      })
    }).catch((error) => {
      console.log(error)
    })
    document.getElementsByClassName('file-show-box')[0].addEventListener('mousewheel', (e) => {
      e.stopPropagation()
      e.preventDefault()
    }, {passive: false})
  },
  methods: {
    swiperResize () {
      this.swiperObj[this.option.propId].update()
    },
    ctrlNode (tag, flag, name) {
      let node = document.createElement('div')
      node.setAttribute('class', name + '-' + this.option.propId + ' ' + name + ' ' + name + '-' + this.option.navigate.type)
      if (this.option.navigate.position === 'outside') {
        document.getElementById(this.option.propId).parentNode.appendChild(node)
      } else {
        document.getElementById(this.option.propId).appendChild(node)
      }
      if (tag === 'el') {
        this.option[flag][tag] = '.' + name
      } else {
        this[flag][tag] = '.' + name + '-' + this.option.propId
      }
    },
    throttle (method, context) {
      clearTimeout(method.tid)
      method.tid = setTimeout(function () {
        method.call(context)
      }, 500)
    },
    checkFile (src, type) {
      this.fileSrc = src
      this.fileType = type
      document.getElementsByClassName(this.option.propId + '-modal')[0].style.display = 'block'
    },
    hideFile () {
      document.getElementsByClassName(this.option.propId + '-modal')[0].style.display = 'none'
    }
  }
}
</script>

<style>
@import "../../static/swiper.min.css";
.swiper-slide-container {
  width: 100%;
  height: 100%;
  display: block;
}
.swiper-container-out {
  padding: 0 50px;
}
.swiper-wrapper {
  position: relative;
  z-index: 998;
}
.swiper-container {
  z-index: initial;
  position: relative;
}
.swiper-container-box {
  width: 100%;
  height: 100%;
  position: relative;
}
.swiper-container-out .swiper-container-box {
  overflow: hidden;
}
.swiper-container>div[class^="swiper-pagination"] {
  position: absolute;
  z-index: 100;
}
.swiper-slide-file {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-content: center;
  align-items: center;
  box-sizing: border-box;
  padding: 10%;
}
.swiper-slide-file img {
  display: block;
}
.swiper-slide-file p {
  text-decoration: underline;
  font-size: 3rem;
  color: #666;
  padding: 1rem;
  cursor: pointer;
}
.file-show-box {
  position: fixed;
  left: 0;
  top: 0;
  z-index: 999;
  width: 100%;
  height: 100%;
  display: none;
  background: rgba(	119, 136, 153, 0.4);
  box-sizing: border-box;
  padding: calc(15% - 1px) calc(25% - 1px);
}
.file-box {
  width: 100%;
  height: 100%;
  background: #fff;
}
.swiper-button-prev, .swiper-container-rtl .swiper-button-next,
.swiper-button-next, .swiper-container-rtl .swiper-button-prev,
.swiper-button-next.swiper-button-disabled, .swiper-button-prev.swiper-button-disabled {
  z-index: 998;
}
.swiper-button-prev,
.navigation-out.swiper-button-prev {
  left: 0
}
.swiper-button-next,
.navigation-out.swiper-button-next {
  right: 0
}
.swiper-container-horizontal>.swiper-pagination-bullets, .swiper-pagination-custom, .swiper-pagination-fraction {
  position: absolute;
  z-index: 998;
}
.swiper-button-prev.swiper-button-prev-large {
  height: 100px;
  width: 50px;
  background: url('../assets/swiper_button_large.png') no-repeat;
  background-position: 0 50%; 
}
.swiper-button-next.swiper-button-next-large {
  height: 100px;
  width: 50px;
  background: url('../assets/swiper_button_large.png') no-repeat;
  background-position: -75px 50%; 
}
.swiper-button-prev.swiper-button-prev-circle {
  height: 32px;
  width: 32px;
  background: url('../assets/swiper_button_circle.png') no-repeat;
  background-position: 0 50%; 
}
.swiper-button-next.swiper-button-next-circle {
  height: 32px;
  width: 32px;
  background: url('../assets/swiper_button_circle.png') no-repeat;
  background-position: -40px 50%; 
}
.swiper-button-prev.swiper-button-prev-bold {
  height: 32px;
  width: 20px;
  background: url('../assets/swiper_button_bold.png') no-repeat;
  background-position: 0 50%; 
}
.swiper-button-next.swiper-button-next-bold {
  height: 32px;
  width: 20px;
  background: url('../assets/swiper_button_bold.png') no-repeat;
  background-position: -30px 50%; 
}
.swiper-button-prev.swiper-button-prev-shadow {
  height: 60px;
  width: 36px;
  background: url('../assets/swiper_button_shadow.png') no-repeat;
  background-position: 0 50%; 
}
.swiper-button-next.swiper-button-next-shadow {
  height: 60px;
  width: 36px;
  background: url('../assets/swiper_button_shadow.png') no-repeat;
  background-position: -75px 50%; 
}
</style>
