<template>
  <div class="box">
    <div>Show: {{ message }}</div>
    <hr>
    <Child_One :msg="message" @update:msg="message = $event"></Child_One>
    <hr>
    <!-- :msg.sync 相当于:msg 与 @update:msg 的组合-->
    <Child_Two :msg.sync="message"></Child_Two>
  </div>
</template>

<script>
import Child_Two from "@/pages/05_sync/Child_Two.vue";
import Child_One from "@/pages/05_sync/Child_One.vue";

// .sync 的实现需要存在 v-bind:数据变量名 与 @update:数据变量名，且数据变量名相同.

// .sync 和 v-model 的选择:
// (一般用于封装组件)当有表单元素的时候一般会使用 v-model，其他情况使用 .sync。
export default {
  name: "SyncTest",
  components: {Child_One, Child_Two},
  data() {
    return {
      message: "message",
    }
  },
}
</script>

<style scoped>

</style>