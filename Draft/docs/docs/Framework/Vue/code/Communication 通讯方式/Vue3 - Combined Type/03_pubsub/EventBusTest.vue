<template>
  <div class="box">
    <h1>组件间通信: pubsub 消息订阅与发布</h1>
    <Child1 />
    <Child2 />
  </div>
</template>

<script lang="ts" setup>
// pubsub 是一个第三方插件，一般用于兄弟组件间的一种通信方式。
import Child1 from './Child_one.vue';
import Child2 from './Child_two.vue';


</script>