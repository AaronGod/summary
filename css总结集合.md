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

- ul>li:last-child 和 ul>li:last-of-type 的区别？
  1.  last-child 是先找到父元素 ， 找到所有的子元素中最后一个 ，判断是不是LI 是就选中，不是就无效选择器
  2. last-of-type  先找到父元素, 找到所有的类型为LI的元素 ，选中最后一个 