<template>
  <layout title="Image" source="image/index.vue" :api="api">
    <div class="components-view">
      <j-code :overview="true" :source="code.overview"></j-code>
    </div>


    <div class="components-view">
      <div class="view-title">基础实例（两种缩放方式）</div>

      <div class="image-line">
        <mod-image class="image-line-item" :ratio="0.5"  src="https://oajua4pqj.qnssl.com/o_1bfbdh2181rcakt21u8uhvg1299r.jpeg">
          <div class="bottom-tip">君の名は - 星海城</div>
        </mod-image>

        <mod-image class="image-line-item" scale="contain" :ratio="0.5" src="https://oajua4pqj.qnssl.com/o_1bfba3u05hj917a9bmkeeq184dc.jpeg" />
      </div>

      <j-code  :source="code.base"></j-code>
    </div>

    <div class="components-view">
      <div class="view-title">手动加载图片，监听加载成功事件，自定义加载中图片</div>
      <div class="image-line">
        <mod-image class="image-line-item" v-on:loaded="onLoaded" :auto="auto" :width="400" :ratio="0.5" src="https://oajua4pqj.qnssl.com/o_1bfbrlmul10k1f946ds2jjgh6c.jpeg?a=1"></mod-image>

        <mod-image class="image-line-item" :auto="auto" scale="contain"
            loading-url="http://localhost:8080/static/img/logo.245c948.jpeg"
            :width="400" :ratio="0.5" src="https://oajua4pqj.qnssl.com/o_1bhj8vas16rk1ffc1jhj1uhc13sg7.png"></mod-image>
      </div>

      <div class="view-actions">
        <mod-button :inline="true" v-on:click="auto = true">加载图片</mod-button>
      </div>

      <j-code  :source="code.event"></j-code>

    </div>


    <div class="components-view">
      <div class="view-title">lazyload 延迟加载（看不清，刷新快速滚动...）</div>
      <mod-image :lazy="true" :width="400" :ratio="0.5" src="https://oajua4pqj.qnssl.com/o_1bfbrlmul10k1f946ds2jjgh6c.jpeg"></mod-image>
      <mod-image :lazy="true" :width="400" :ratio="0.5" src="https://oajua4pqj.qnssl.com/o_1bfbb16e01a8b68f162d18c11qt9m.jpeg"></mod-image>
      <mod-image :lazy="true" :width="400" :ratio="0.5" src="https://oajua4pqj.qnssl.com/o_1bfbasnqvfrin0o1cr9go2104qc.jpeg"></mod-image>
      <mod-image :lazy="true" :width="400" :ratio="0.5" src="https://oajua4pqj.qnssl.com/o_1bhto5e7k15lq1j3513ufjtv1gfr7.png"></mod-image>

      <j-code  :source="code.lazy"></j-code>

    </div>


    <div class="components-view">
      <div class="view-title">加载失败和自定义加载失败</div>

      <div class="image-line">
        <mod-image class="image-line-item" :ratio="0.5"  src="https://oajua4pqj.qnssl.com/o_1bfbdh2181rcakt21u8uhvg1299r1.jpeg"></mod-image>

        <mod-image class="image-line-item" scale="contain" :ratio="0.5" src="https://oajua4pqj.qnssl.com/o_1bfba3u05hj917a9bmkeeq184dc.jpeg11" >
          <div class="custom-error" slot="error">😔 图片挂了宝宝 😢</div>
        </mod-image>
      </div>

      <j-code  :source="code.error"></j-code>
    </div>


    <div class="components-view">
      <div class="view-title">在弹层中的图片</div>

      <mod-alert v-model="show1">
        <mod-image :width="400" :ratio="0.5" src="https://oajua4pqj.qnssl.com/o_1bhto5e7k15lq1j3513ufjtv1gfr7.png"></mod-image>
      </mod-alert>

      <mod-button :inline="true" v-on:click="show1 = true">点击显示</mod-button>

      <j-code  :source="code.dialog"></j-code>

    </div>

    <div class="components-view">
      <p class="view-title">图片，宽高，缩放样式修改</p>

      <mod-image class="image-has-background" :clickReload="true" :ratio="ratio" v-bind:src="src" :scale="scale" :width="400"/>

      <div class="view-actions">
        <mod-button :inline="true" v-on:click="changeImage">切换图片</mod-button>
        <mod-button :inline="true" v-on:click="(ratio = ratio == 0.5 ? 1 : 0.5)">切换容器比例</mod-button>
        <mod-button :inline="true" v-on:click="(scale = scale == 'cover' ? 'contain' : 'cover')">切换缩放方式</mod-button>
      </div>

      <j-code  :source="code.change"></j-code>

    </div>

  </layout>
</template>

<script>
  import Layout from '../common/common_layout';
  import code from './index.ch';
  import api from './index.ch.api.md';

  const IMAGE1 = 'https://oajua4pqj.qnssl.com/o_1bfbasnqvfrin0o1cr9go2104qc.jpeg'
  const IMAGE2 = 'https://oajua4pqj.qnssl.com/o_1bfbb16e01a8b68f162d18c11qt9m.jpeg'

  export default {
    components: {
      Layout
    },
    data () {
      return {
        api: api,
        code: code,
        img: 1,
        ratio: 0.5,
        scale: 'cover',
        auto: false,
        show1: false
      }
    },
    methods: {
      changeImage () {
        this.img = !this.img;
      },

      onLoaded () {
        this.$jsmod.toast.show({
          type: 'success',
          content: '图片加载成功'
        });
      }
    },
    computed: {
      src () {
        return this.img ? IMAGE1 : IMAGE2;
      }
    }
  }
</script>

<style lang="stylus">
  @import "~website/assets/mixin"

  .bottom-tip
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    background: rgba(0, 0, 0, 0.7);
    color: #fff;
    padding: 10px;
    font-size: 12px;

  .image-line
    display: flex;

    .image-line-item
      flex: 1 1 auto;
      width: 0;
      background: #efefef;

  .custom-error
    text-align: center;
    padding-top: 30px;
    color: #ff5a00;
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    background: main-color;
    color: #fff;

  .image-has-background
    background: #efefef;
    border: 1px solid main-color;

</style>
