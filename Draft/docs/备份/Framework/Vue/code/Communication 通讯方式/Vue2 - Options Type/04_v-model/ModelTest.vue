<template>
  <div class="box">
    <h3>关于标签</h3>
    <div>Value: {{ value || "稍微等待一会儿..." }}</div>
    <label> v-model 双向数据绑定:
      <input type="text" v-model="value">
    </label>

    <br><br>
    <button @click="change_value"> change_value </button>

    <!---------------------------------------------------->
    <hr>
    <h3> v-bind  && @input 实现 v-model </h3>
    <div>Keyword: {{ keyword || "稍微等待一会儿..." }}</div>
    <br>
    <!--
    @change 是输入框内容改变且失去焦点才会触发,
    @input 是在文本框的 value 发生改变时，就会触发
    -->
    <label> v-bind 单向数据绑定:
      <input type="text" :value="keyword" @input="changeInput">
    </label>
    <!--<input type="text" v-model:value="value">-->

    <!---------------------------------------------------->
    <hr>
    <!-- v-model 用于父子组件间的数据同步 -->
    <h3>关于组件</h3>
    <!-- 通过 v-bind 数据绑定 与 @input 自定义事件实现 v-model 的效果 -->
    <CustomInput :value="value" @input="value = $event "></CustomInput>

    <!--此处的 v-model 是 :value 与 @input 的结合替换-->
    <CustomInput v-model="value"></CustomInput>


  </div>
</template>

<script>
import CustomInput from "@/pages/04_v-model/CustomInput.vue";

export default {
  name: "ModelTest",
  components: {CustomInput},
  data() {
    return {
      value: "",
      keyword: "",
    }
  },
  methods: {
    change_value(){
      this.value += "h";
    },
    changeInput(e){
      this.keyword = e.target.value;
    },
  }
}
</script>

<style lang="less" scoped>

</style>