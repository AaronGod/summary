#### 1.布局总结

- list 图文

![1654739828486](assets/1654739828486.png)

~~~html
<ul>
        <li>
          <img src="https://yanxuan-item.nosdn.127.net/6f7a6c3ccc8cd0b1fb8446db90099446.png" alt="">
          <div class="info">
            <p class="name ellipsis-2">【定金购】严选零食大礼包（12件）</p>
            <p class=""></p>
            <p class="price"></p>
          </div>
        </li>
 </ul>
~~~

- 轮播图

  ~~~vue
  <template>
    <div class="ebird-carousel">
      <ul class="carousel-body" v-if="list && list.length">
        <li class="carousel-item" v-for="(slide,i) in list" :key="slide.id" :class="{fade: index === i}">
          <router-link to="/">
            <img :src="slide.imgUrl" alt="">
          </router-link>
        </li>
      </ul>
      <!-- 左右箭头 -->
      <a href="javascript:;" class="carousel-btn prev"><i class="iconfont icon-angle-left"></i></a>
      <a href="javascript:;" class="carousel-btn next"><i class="iconfont icon-angle-right"></i></a>
      <!-- 指示器 -->
      <div class="carousel-indicator">
        <span v-for="(slide,i) in list" :key="slide.id" :class="{active: index === i}"></span>
      </div>
    </div>
  </template>
  
  <script>
  import { onUnmounted, ref, watch } from 'vue'
  export default {
    name: 'ebird-carousel',
    props: {
      // 轮播图数据
      list: {
        type: Array,
        default: () => []
      },
      autoPlay: {
        type: Boolean,
        default: true
      },
      // 图片停留时长
      duration: {
        type: Number,
        default: 3000
      }
    },
    setup (props) {
      // 当前的显示图索引
      const index = ref(0)
      // 自动播放
      // 定时器
      let timer = null
      const autoPlayFn = () => {
        clearInterval(timer)
        timer = setInterval(() => {
          index.value++
          if (index.value > props.list.length - 1) {
            index.value = 0
          }
        }, props.duration)
        // if (props.autoPlay) {
        // }
      }
  
      // 开启自动播放条件： 有数据&开启自动播放，才调用自动播放函数
      watch(() => props.list, newVal => {
        if (newVal.length && props.autoPlay) {
          index.value = 0
          autoPlayFn()
        }
      }, { immediate: true })
  
      // 鼠标移入暂停  移除开始
      const start = () => {
        if (props.list.length && props.autoPlay) {
          autoPlayFn()
        }
      }
      const stop = () => {
        if (timer) {
          clearInterval(timer)
        }
      }
  
      // 上一张 ，下一张 切换
      const toggle = (step) => {
        const newIndex = index.value + step
        if (newIndex > props.list.length - 1) {
          index.value = 0
          return
        }
        if (newIndex < 0) {
          index.value = props.list.length - 1
          return
        }
        index.value = newIndex
      }
  
      // 组件销毁清除定时器
      onUnmounted(() => {
        clearInterval(timer)
      })
      return { index, start, stop, toggle }
    }
  }
  </script>
  ~~~

- list 图文2

  ![1655346120768](assets/1655346120768.png)

~~~vue
<ul class="goods-list">
        <li v-for="item in goods" :key="item.id">
          <RouterLink :to="`/product/${item.id}`">
            <img :src="item.picture" alt="">
            <p class="name ellipsis">{{item.name}}</p>
            <p class="price">&yen;{{item.price}}</p>
          </RouterLink>
        </li>
      </ul>
~~~

- 图文布局3

  ![65545804657](assets/1655458046572.png)

  ~~~html
  <!-- 单个item -->
  <div class="goods-item">
      <RouterLink to="/" class="image">
        <img src="http://zhoushugang.gitee.io/erabbit-client-pc-static/uploads/fresh_goods_1.jpg" alt="" />
      </RouterLink>
      <p class="name ellipsis-2">美威 智利原味三文鱼排 240g/袋 4片装</p>
      <p class="desc">海鲜年货</p>
      <p class="price">&yen;108.00</p>
      <div class="extra">
        <RouterLink to="/">
          <span>找相似</span>
          <span>发现现多宝贝 &gt;</span>
        </RouterLink>
      </div>
    </div>
  ~~~

  ![65547751649](assets/1655477516494.png)

~~~html
<!-- 左右布局   ，左边固定一个高度  ，右边每个为左边二分之一 加上 中间间隔高度，
右边每个li 设置一个margin-bottom  最后一排margin-bottom设置为0
-->
<style>
 .goods-list {
      width: 990px;
      display: flex;
      flex-wrap: wrap;
      li {
        width: 240px;
        height: 300px;
        margin-right: 10px;
        margin-bottom: 10px;
        &:nth-last-child(-n+4) {
          margin-bottom: 0;
        }
        &:nth-child(4n) {
          margin-right: 0;
        }
      }
    }
</style>
~~~

![65547964068](assets/1655479640683.png)

~~~vue
    <div class="special-list" ref="homeSpecial">
      <div class="special-item" v-for="i in 3" :key="i">
        <RouterLink to="/">
          <img src="http://zhoushugang.gitee.io/erabbit-client-pc-static/uploads/topic_goods_1.jpg" alt />
          <div class="meta">
            <p class="title">
              <span class="top ellipsis">看到撒娇的撒娇的凯撒就</span>
              <span class="sub ellipsis">倒萨倒萨倒萨</span>
            </p>
            <span class="price">&yen;19.99起</span>
          </div>
        </RouterLink>
        <div class="foot">
          <span class="like"><i class="iconfont icon-hart1"></i>100</span>
          <span class="view"><i class="iconfont icon-see"></i>100</span>
          <span class="reply"><i class="iconfont icon-message"></i>100</span>
        </div>
      </div>
    </div>
<style scoped lang='less'>
.special-list {
  height: 380px;
  padding-bottom: 20px;
  display: flex;
  justify-content: space-between;
  .special-item {
    width: 404px;
    background: #fff;
    .hoverShadow();
    a {
      display: block;
      width: 100%;
      height: 288px;
      position: relative;
      img {
        width: 100%;
        height: 100%;
      }
      .meta {
        background-image: linear-gradient(to top,rgba(0, 0, 0, 0.8),transparent 50%);
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 288px;
        .title {
          position: absolute;
          bottom: 0px;
          left: 0;
          padding-left: 16px;
          width: 70%;
          height: 70px;
          .top {
            color: #fff;
            font-size: 22px;
            display: block;
          }
          .sub {
            display: block;
            font-size: 19px;
            color: #999;
          }
        }
        .price {
          position: absolute;
          bottom: 25px;
          right: 16px;
          line-height: 1;
          padding: 4px 8px 4px 7px;
          color: @priceColor;
          font-size: 17px;
          background-color: #fff;
          border-radius: 2px;
        }
      }
    }
    .foot {
      height: 72px;
      line-height: 72px;
      padding: 0 20px;
      font-size: 16px;

      i {
        display: inline-block;
        width: 15px;
        height: 14px;
        margin-right: 5px;
        color: #999;
      }
      .like,
      .view {
        float: left;
        margin-right: 25px;
        vertical-align: middle;
      }
      .reply {
        float: right;
        vertical-align: middle;
      }
    }
  }
}
</style>
~~~

