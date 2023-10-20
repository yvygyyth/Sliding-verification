<template>
  <div class="flex">
    <div id="captcha"></div>
  </div>
</template>

<script>
import './jigsaw.js'
export default {
    props: {
      dragVerifyCode: {
      type: [String,Boolean], 
      // default: false, // 设置默认值为 0
      require:true,
    },
    dragVerifyVisible:{
      type: [Boolean], 
    }
  },
  emits: ['update:dragVerifyCode','update:dragVerifyVisible'],
  mounted(){
    window.jigsaw.init({
      el: document.getElementById("captcha"), // 传入容器元素
      width: 310, // 可选, 默认310
      height: 155, // 可选, 默认155
      onSuccess: () => {
        this.dragVerifyCodeUpdate(true)
        this.dragVerifyVisibleUpdata(false)
        // 在验证通过后执行的逻辑
      },
      onFail: () => {
        this.dragVerifyCodeUpdate(false)
        // 在验证失败后执行的逻辑
      },
      onRefresh: () => {
        this.dragVerifyCodeUpdate(false)
        // 在点击刷新时执行的逻辑
      }
    });
  },
  methods:{
    dragVerifyCodeUpdate(code){
      this.$emit('update:dragVerifyCode', code);
    },
    dragVerifyVisibleUpdata(vis){
      this.$emit('update:dragVerifyVisible',vis)
    }
  }
}
</script>

<style>
.flex{
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>