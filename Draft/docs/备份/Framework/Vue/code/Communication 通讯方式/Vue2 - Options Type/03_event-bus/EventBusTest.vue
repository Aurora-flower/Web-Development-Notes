<template>
  <div class="box">
    <Child_One></Child_One>
    <hr>
    <Child_Two></Child_Two>
  </div>
</template>

<script>

// 事件总线 - 用于跨组件间的通信
import Child_One from "@/pages/03_event-bus/Child_One.vue";
import Child_Two from "@/pages/03_event-bus/Child_Two.vue";

export default {
  name: "EventBusTest",
  components: {
    Child_One,
    Child_Two,
  },
}
</script>

<style scoped>

</style>