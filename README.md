# 轮播组件

## 当前可配置功能
- 基础轮播
- 宽度高度设置带单位
- 自动轮播
- 分页器
- 分页器自定义
- 前进后退按钮
- 前进后退按钮自定义
- loop循环
- 懒加载
- 多栏轮播
- 多栏轮播间隔设置
- 垂直、水平方向轮播
- 卡片式轮播
- 联动轮播
- 增删栏目
- 带文件轮播（展示为icon，点击预览）
- 加载更多功能

---

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev
```
---
## 使用

### 引入
``` javascript
import Swiper from '../common/swipe'
import SwiperGroup from '../common/swipe-group' //需要联动功能时引入
```
#### 基础示例
``` HTML
    <c-swiper :propOption='options.swipeBoxNormal' :listData='listData'></c-swiper>
```
#### 联动示例
``` HTML
    <c-swiper-group :propOption='groupOptions.swipeGroupHon.option'>
      <c-swiper v-for="(item, key) in groupOptions.swipeGroupHon.items" :key="item.propId" :propOption='item.option':listData='item.listData'></c-swiper>
    </c-swiper-group>
```
#### 传入数据示例
``` javascript
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
          type: 'audio',
          src: '../../static/4.mp3'
        },
        {
          type: 'video',
          src: '../../static/5.avi'
        },
        {
          type: 'txt',
          src: '../../static/6.txt'
        },
        {
          type: 'pdf',
          src: '../../static/7.pdf'
        }
      ]
```
#### 传入配置示例
``` javascript
      options: {
        swipeBoxNormal: {
          propId: 'swipeBoxNormal',
          height: '30rem',
          width: '90rem'
        }
      }
```
---
# 配置项
## Attribute
## swipe-item
<table border width="100%">
  <thead>
    <tr>
      <th>attr Object</th>
      <th>attr name</th>
      <th>attr</th>
      <th>description</th>
      <th>default</th>
      <th>Value</th>
      <th>required</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan='24'>propOption</td>
      <td>height</td>
      <td rowspan='15'> </td>
      <td>轮播组件容器高度</td>
      <td>100%</td>
      <td>String</td>
      <td>false</td>
    </tr>
    <tr>
      <td>width</td>
      <td>轮播组件容器宽度</td>
      <td>100%</td>
      <td>String</td>
      <td>false</td>
    </tr>
    <tr>
      <td>propId</td>
      <td>轮播组件容器ID，后续作为唯一标识</td>
      <td>''</td>
      <td>String</td>
      <td>true</td>
    </tr>
    <tr>
      <td>listData</td>
      <td>数据内容</td>
      <td>[ ]</td>
      <td>Array</td>
      <td>false</td>
    </tr>
    <tr>
      <td>slidesPerView</td>
      <td>当前容器内显示的可见栏数量</td>
      <td>1</td>
      <td>Number</td>
      <td>false</td>
    </tr>
    <tr>
      <td>spaceBetween</td>
      <td>分栏显示时，栏目之间的间隔</td>
      <td>0</td>
      <td>Number</td>
      <td>false</td>
    </tr>
    <tr>
      <td>direction</td>
      <td>轮播方向</td>
      <td>horizontal</td>
      <td>horizontal,vertical</td>
      <td>false</td>
    </tr>
    <tr>
      <td>initialSlide</td>
      <td>加载后显示的栏目索引</td>
      <td>0</td>
      <td>Number</td>
      <td>false</td>
    </tr>
    <tr>
      <td>speed</td>
      <td>轮播速度</td>
      <td>300</td>
      <td>Number</td>
      <td>false</td>
    </tr>
    <tr>
      <td>preloadImages</td>
      <td>是否预加载</td>
      <td>true</td>
      <td>Boolean</td>
      <td>false</td>
    </tr>
    <tr>
      <td>effect</td>
      <td>轮播效果</td>
      <td>slide</td>
      <td>slide(普通切换、默认)，fade(淡入)，cube(方块)，coverflow(3d流)，flip(3d翻转)</td>
      <td>false</td>
    </tr>
    <tr>
      <td>loop</td>
      <td>是否可以循环轮播</td>
      <td>false</td>
      <td>Boolean</td>
      <td>false</td>
    </tr>
    <tr>
      <td>observer</td>
      <td>监听器，是否可以动态添加栏目</td>
      <td>false</td>
      <td>Boolean</td>
      <td>false</td>
    </tr>
    <tr>
      <td>autoplay</td>
      <td>是否开启自动轮播</td>
      <td>false</td>
      <td>Boolean</td>
      <td>false</td>
    </tr>
    <tr>
      <td>delay</td>
      <td>自动轮播延迟</td>
      <td>3000</td>
      <td>String, Number</td>
      <td>false</td>
    </tr>
    <tr>
      <td rowspan='4'>pagination</td>
    </tr>
    <tr>
      <td>type</td>
      <td>分页器功能-分页器样式</td>
      <td>bullets</td>
      <td>
        ‘bullets’  圆点（默认）
        ‘fraction’  分式 
        ‘progressbar’  进度条
        ‘custom’ 自定义
      </td>
      <td>false</td>
    </tr>
    <tr>
      <td>dynamicBullets</td>
      <td>分页器功能-动态分页器，数量多时会隐藏</td>
      <td>false</td>
      <td>Boolean</td>
      <td>false</td>
    </tr>
    <tr>
      <td>clickable</td>
      <td>分页器功能-分页器是否可点击</td>
      <td>true</td>
      <td>Boolean</td>
      <td>false</td>
    </tr>
    <tr>
      <td>bulletsColor</td>
      <td> </td>
      <td>分页样式pagination.type为bullets时，设置小点背景色</td>
      <td>#007aff</td>
      <td>String</td>
      <td>false</td>
    </tr>
    <tr>
      <td rowspan='3'>navigate</td>
    </tr>
    <tr>
      <td>position</td>
      <td>前进后退按钮在容器中位置</td>
      <td>inside</td>
      <td>inside, outside</td>
      <td>false</td>
    </tr>
    <tr>
      <td>type</td>
      <td>前进后退按钮的样式类型</td>
      <td>default</td>
      <td>default, circle, large, bold, shadow</td>
      <td>false</td>
    </tr>
    <tr>
      <td>lazy</td>
      <td></td>
      <td>是否懒加载</td>
      <td>false</td>
      <td>Boolean</td>
      <td>false</td>
    </tr>
  </tbody>
</table>

## Events
### 加载更多功能
``` HTML
    <c-swiper :propOption='options.swipeBoxMore' @last='loadmore' :listData='listDataMore'></c-swiper>
```
> last事件 关联于加载更多功能，当轮播组件滑动至最后一张时触发，需要执行当前引用组件的methods中的方法(loadmore)，对传入prop.listData的字段(listDataMore)二次赋值，继而更新视图

## swipe-group
<table border width="100%">
  <thead>
    <tr>
      <th>attr Object</th>
      <th>attr name</th>
      <th>description</th>
      <th>default</th>
      <th>Value</th>
      <th>required</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan='5'>propOption</td>
    </tr>
    <tr>
      <td>height</td>
      <td>轮播组件容器高度</td>
      <td>100%</td>
      <td>String</td>
      <td>false</td>
    </tr>
    <tr>
      <td>width</td>
      <td>轮播组件容器宽度</td>
      <td>100%</td>
      <td>String</td>
      <td>false</td>
    </tr>
    <tr>
      <td>direction</td>
      <td>联动组件的排列方式</td>
      <td>horizontal</td>
      <td>String</td>
      <td>horizontal，vertical</td>
    </tr>
    <tr>
      <td>align</td>
      <td>相对于group容器，在内部排列的方式，flex布局中的justify-content</td>
      <td>around</td>
      <td>around，between</td>
      <td>false</td>
    </tr>
  </tbody>
</table>
