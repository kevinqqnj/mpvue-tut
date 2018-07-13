<template>
	<div>
	<map></map>
		<camera device-position="back" flash="off" style="width: 100%; height: 300px;"></camera>
<button type="primary" @click="takePhoto">拍照</button>
<view>预览</view>
<image mode="widthFix" :src="src"></image>

  <div class="counter-warp">
    
    <p>Vuex counter：{{ count }}</p>
    <p>
      <button @click="increment">+</button>
      <button @click="decrement">-</button>
    </p>

    <a href="/pages/index/main" class="home">去往首页</a>
  </div>
  		</div>
</template>

<script>
// Use Vuex
import store from './store'

export default {
	  data () {
    return {
      src: '',
    }
  },
  computed: {
    count () {
      return store.state.count
    }
  },
  methods: {
    takePhoto() {
        const ctx = wx.createCameraContext()
        ctx.takePhoto({
            quality: 'high',
            success: (res) => {
                this.src = res.tempImagePath
            }
        })
    },
    increment () {
      store.commit('increment')
    },
    decrement () {
      store.commit('decrement')
    },
  }
}
</script>

<style>
.counter-warp {
  text-align: center;
  margin-top: 100px;
}
.home {
  display: inline-block;
  margin: 100px auto;
  padding: 5px 10px;
  color: blue;
  border: 1px solid blue;
}
</style>
