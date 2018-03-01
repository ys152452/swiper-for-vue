<template>
  <div class="hello">
    <h6>正常</h6>
    <c-swiper :propOption='options.swipeBoxNormal' :listData='listData'></c-swiper>
    <h6>响应式</h6>
    <c-swiper :propOption='options.swipeBoxFit' :listData='listData'></c-swiper>
    <h6>auto</h6>
    <c-swiper :propOption='options.swipeBoxAuto' :listData='listData'></c-swiper>
    <h6>分页器</h6>
    <c-swiper :propOption='options.swipeBoxPage' :listData='listData'></c-swiper>
    <h6>分页器颜色</h6>
    <c-swiper :propOption='options.swipeBoxPageColor' :listData='listData'></c-swiper>
    <h6>分页器样式</h6>
    <c-swiper :propOption='options.swipeBoxPageType' :listData='listData'></c-swiper>
    <h6>前进后退</h6>
    <c-swiper :propOption='options.swipeBoxNavi' :listData='listData'></c-swiper>
    <h6>前进后退外置</h6>
    <c-swiper :propOption='options.swipeBoxNaviOut' :listData='listData'></c-swiper>
    <h6>前进后退样式</h6>
    <c-swiper :propOption='options.swipeBoxNaviOutExp' :listData='listData'></c-swiper>
    <h6>环路</h6>
    <c-swiper :propOption='options.swipeBoxLoop' :listData='listData'></c-swiper>
    <h6>lazy</h6>
    <c-swiper :propOption='options.swipeBoxLazy' :listData='listData'></c-swiper>
    <h6>三栏显示</h6>
    <c-swiper :propOption='options.swipeBoxPre' :listData='listData'></c-swiper>
    <h6>三栏分隔显示</h6>
    <c-swiper :propOption='options.swipeBoxSpace' :listData='listData'></c-swiper>
    <h6>垂直滚动</h6>
    <c-swiper :propOption='options.swipeBoxVertical' :listData='listData'></c-swiper>
    <h6>卡片化</h6>
    <c-swiper :propOption='options.swipeBoxCard' :listData='listData'></c-swiper>
    <h6>联动水平</h6>
    <c-swiper-group :propOption='groupOptions.swipeGroupHon.option'>
      <c-swiper v-for="(item, key) in groupOptions.swipeGroupHon.items" :key="item.propId" :propOption='item.option':listData='item.listData'></c-swiper>
    </c-swiper-group>
    <h6>联动垂直</h6>
    <c-swiper-group :propOption='groupOptions.swipeGroupArd.option'>
      <c-swiper v-for="(item, key) in groupOptions.swipeGroupArd.items" :key="item.propId" :propOption='item.option':listData='item.listData'></c-swiper>
    </c-swiper-group>
    <h6>observer动态</h6>
    <c-swiper :propOption='options.swipeBoxObserver' :listData='listData'></c-swiper>
    <button @click='observer'>删除第一个</button>
    <h6>文件</h6>
    <c-swiper :propOption='options.swipeBoxMix' :listData='listDataMix'></c-swiper>
    <h6>加载更多</h6>
    <c-swiper :propOption='options.swipeBoxMore' @last='loadmore' :listData='listDataMore'></c-swiper>
  </div>
</template>
<script>
import Swiper from '../common/swipe'
import SwiperGroup from '../common/swipe-group'
export default {
  name: 'index',
  components: {
    'c-swiper': Swiper,
    'c-swiper-group': SwiperGroup
  },
  data () {
    return {
      options: {
        swipeBoxNormal: {
          propId: 'swipeBoxNormal',
          height: '30rem',
          width: '90rem'
        },
        swipeBoxFit: {
          propId: 'swipeBoxFit',
          height: '30rem',
          width: '80%'
        },
        swipeBoxAuto: {
          propId: 'swipeBoxAuto',
          height: '30rem',
          width: '90rem',
          autoplay: true,
          delay: 1000
        },
        swipeBoxPage: {
          propId: 'swipeBoxPage',
          height: '30rem',
          width: '90rem',
          pagination: {
            type: 'bullets',
            dynamicBullets: false,
            clickable: true
          }
        },
        swipeBoxPageType: {
          propId: 'swipeBoxPageType',
          height: '30rem',
          width: '90rem',
          pagination: {
            type: 'fraction',
            dynamicBullets: false,
            clickable: true
          }
        },
        swipeBoxPageColor: {
          propId: 'swipeBoxPageColor',
          height: '30rem',
          width: '90rem',
          pagination: {
            type: 'bullets',
            dynamicBullets: false,
            clickable: true
          },
          bulletsColor: '#000'
        },
        swipeBoxNavi: {
          propId: 'swipeBoxNavi',
          height: '30rem',
          width: '90rem',
          navigate: {}
        },
        swipeBoxNaviOut: {
          propId: 'swipeBoxNaviOut',
          height: '30rem',
          width: '90rem',
          navigate: {
            position: 'outside',
            type: 'default'
          }
        },
        swipeBoxNaviOutExp: {
          propId: 'swipeBoxNaviOutExp',
          height: '30rem',
          width: '90rem',
          navigate: {
            position: 'outside',
            type: 'shadow'
          }
        },
        swipeBoxLoop: {
          propId: 'swipeBoxLoop',
          height: '30rem',
          width: '90rem',
          loop: true
        },
        swipeBoxLazy: {
          propId: 'swipeBoxLazy',
          height: '30rem',
          width: '90rem',
          lazy: true
        },
        swipeBoxPre: {
          propId: 'swipeBoxPre',
          height: '30rem',
          width: '90rem',
          slidesPerView: 3
        },
        swipeBoxSpace: {
          propId: 'swipeBoxSpace',
          height: '30rem',
          width: '90rem',
          slidesPerView: 3,
          spaceBetween: 20
        },
        swipeBoxVertical: {
          propId: 'swipeBoxVertical',
          height: '30rem',
          width: '90rem',
          direction: 'vertical'
        },
        swipeBoxCard: {
          propId: 'swipeBoxCard',
          height: '30rem',
          width: '90rem',
          slidesPerView: 3,
          effect: 'coverflow'
        },
        swipeBoxObserver: {
          propId: 'swipeBoxObserver',
          height: '30rem',
          width: '90rem',
          observer: true
        },
        swipeBoxMix: {
          propId: 'swipeBoxMix',
          height: '30rem',
          width: '90rem',
          hasFile: true
        },
        swipeBoxMore: {
          propId: 'swipeBoxMore',
          height: '30rem',
          width: '90rem',
          pagination: {
            type: 'bullets',
            dynamicBullets: false,
            clickable: true
          }
        }
      },
      groupOptions: {
        swipeGroupArd: {
          option: {
            height: '60rem',
            width: '70rem',
            direction: 'vertical'
          },
          items: [
            {
              option: {
                propId: 'swipeBoxLinkedArd',
                height: '40%',
                width: '100%'
              },
              listData: [
                {
                  type: 'img',
                  src: '../../static/1.png'
                },
                {
                  type: 'img',
                  src: '../../static/2.png'
                },
                {
                  type: 'img',
                  src: '../../static/3.png'
                },
                {
                  type: 'img',
                  src: '../../static/4.png'
                },
                {
                  type: 'img',
                  src: '../../static/5.png'
                }
              ]
            },
            {
              option: {
                propId: 'swipeBoxLinkArd',
                height: '40%',
                width: '100%'
              },
              listData: [
                {
                  type: 'img',
                  src: '../../static/1.png'
                },
                {
                  type: 'img',
                  src: '../../static/2.png'
                },
                {
                  type: 'img',
                  src: '../../static/3.png'
                },
                {
                  type: 'img',
                  src: '../../static/4.png'
                },
                {
                  type: 'img',
                  src: '../../static/5.png'
                }
              ]
            }
          ]
        },
        swipeGroupHon: {
          option: {
            height: '28rem',
            width: '90rem',
            align: 'between'
          },
          items: [
            {
              option: {
                propId: 'swipeBoxLinkedVer',
                loop: true,
                height: '100%',
                width: '40%'
              },
              listData: [
                {
                  type: 'img',
                  src: '../../static/1.png'
                },
                {
                  type: 'img',
                  src: '../../static/2.png'
                },
                {
                  type: 'img',
                  src: '../../static/3.png'
                },
                {
                  type: 'img',
                  src: '../../static/4.png'
                },
                {
                  type: 'img',
                  src: '../../static/5.png'
                }
              ]
            },
            {
              option: {
                propId: 'swipeBoxLinkVer',
                loop: true,
                height: '100%',
                width: '40%'
              },
              listData: [
                {
                  type: 'img',
                  src: '../../static/1.png'
                },
                {
                  type: 'img',
                  src: '../../static/2.png'
                },
                {
                  type: 'img',
                  src: '../../static/3.png'
                },
                {
                  type: 'img',
                  src: '../../static/4.png'
                },
                {
                  type: 'img',
                  src: '../../static/5.png'
                }
              ]
            }
          ]
        }
      },
      listData: [
        {
          type: 'img',
          src: '../../static/1.png'
        },
        {
          type: 'img',
          src: '../../static/2.png'
        },
        {
          type: 'img',
          src: '../../static/3.png'
        },
        {
          type: 'img',
          src: '../../static/4.png'
        },
        {
          type: 'img',
          src: '../../static/5.png'
        }
      ],
      listDataMix: [
        {
          type: 'img',
          src: '../../static/1.png'
        },
        {
          type: 'pdf',
          src: '../../static/helloworld.pdf'
        },
        {
          type: 'txt',
          src: '../../static/swiper.txt'
        },
        {
          type: 'video',
          src: 'http://www.w3school.com.cn/i/movie.ogg'
        },
        {
          type: 'txt',
          src: '../../static/test.txt'
        }
      ],
      listDataMore: [
        {
          type: 'img',
          src: '../../static/1.png'
        },
        {
          type: 'img',
          src: '../../static/2.png'
        },
        {
          type: 'img',
          src: '../../static/3.png'
        },
        {
          type: 'img',
          src: '../../static/4.png'
        },
        {
          type: 'img',
          src: '../../static/5.png'
        }
      ]
    }
  },
  methods: {
    loadmore () {
      this.listDataMore = [...this.listDataMore, ...this.listData]
    },
    observer () {
      document.getElementById('swipeBoxObserver').getElementsByClassName('swiper-slide')[0].remove()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
button {
  width: 8rem;
  height: 4rem;
  border: 0;
  background: lightblue;
  font-size: 2rem;
  border-radius: 4px;
  margin: 1rem;
}
.hello>div{
  margin: 0 auto;
}
</style>
