<template>
  <div class="box">
    <h3>需求: （封装）自定义带 Hover 提示的按钮</h3>
    <HintButton
        title="Warn"
        content="这是一个删除按钮"
        icon="el-icon-delete"
        type="danger"
        @click.native="clickHandler"
    ></HintButton>
  </div>
</template>

<script>
import HintButton from "@/pages/06_attrs-listeners/HintButton.vue";

export default {
  name: "AttrsListenersTest",
  components: {HintButton},
  methods:{
    clickHandler(){
      console.log(">>> clickHandler");
    }
  }
}
</script>

<style scoped>

</style>