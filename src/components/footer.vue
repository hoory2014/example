<template>
  <div>
    <p v-on:click="hello">{{msg}}</p>
  </div>
</template>
<script>
  export default {
    data () {
      return {
        msg: '©2016 coderYin 苏ICP备15056083号-1 All rights reserved.'
      }
    },
    methods:{
      hello: function(){
        alert("hello world");
        this.msg="我被点击啦";
      }
    }
  }
</script>
