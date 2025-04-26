<template>
  <div class="box">
    <!-- 此时，传递的是属性，尚未绑定父组件的数据 -->
    <!--<h3>>> 传递普通属性</h3>-->
    <!--<Child message="message"></Child>-->
    <!--<hr>-->

    <!-- v-bind 绑定基本数据类型 -->
    <!--<h3>>> v-bind 传递基本数据类型</h3>-->
    <!--<Child :value="value"></Child>-->
    <!--<hr>-->

    <!-- v-bind 绑定引用数据类型 -->
    <!--<h3>>> v-bind 传递引用数据类型</h3>-->
    <!--<Child :obj="obj"></Child>-->
    <!--<hr>-->

    <!-- v-bind 绑定函数类型 - 为使子组件可以调用函数修改父组件的数据 -->
    <!--<h3> v-bind 传递函数类型</h3>-->
    <!--<Child :fun_test="fun_test"></Child>-->
    <!--<hr>-->

    <!---------------------------------------------------->
    <h3>Father</h3>
    <div> value: {{ value }}</div>
    <div> object: name - {{ obj.name }} | age - {{obj.age}}</div>
    <button @click="add"> 自增 </button>
    <button @click="sub"> 自减 </button>
    <br>
    <button @click="changeAddress"> 修改数据_地址层 </button>
    <button @click="changeAttribute"> 修改数据_属性层 </button>
    <br>
    <!--默认传递的第一个参数就是 $event-->
    <button @click="fun_test">fun_test</button>
    <hr>
    <!---------------------------------------------------->
    <!--
    第一种情况:  普通属性
    第二种情况:  v-bind 单向数据流 (非函数类型用来展示)
    第三种情况:  v-bind 单向数据流 (函数类型)
    -->
    <Child message="message" :value="value"
           :add="add" :sub="sub"
           :change-address="changeAddress"
           :change-attribute="changeAttribute"
           :fun_test="fun_test" :obj="obj"
    ></Child>
  </div>
</template>

<script>
import Child from "@/pages/01_props/Child.vue";
export default {
  name: "PropsTest",
  /*
  Tip: vue 中组件是用来复用的，为了防止 data 复用，将其定义为函数。
  vue组件中的 data 数据都应该是相互隔离，互不影响的，组件每复用一次，data 数据就应该被复制一次.
  之后，当某一处复用的地方组件内 data 数据被改变时，其他复用地方组件的 data 数据不受影响，
  就需要通过 data 函数返回一个对象作为组件的状态。
  类似于给每个组件实例创建一个私有的数据空间，让各个组件实例维护各自的数据。
  */
  data(){
    return {
      // 基本数据类型
      value: 1,
      // 引用数据类型
      obj: {
        name: "HuaYin",
        age: 22,
      },

    }
  },
  components: {
    Child
  },
  methods: {
    fun_test(e){
      console.log(e.target);
      console.log(this);
    },
    add(){
      this.value++;
    },
    sub(){
      this.value--;
    },
    changeAddress(){
      this.obj = {
        name: "花楹一间",
        age: 23
      }
    },
    changeAttribute(){
      this.obj.name = "花楹树下";
      this.obj.age = 24;
    },
  }
}
</script>

<style lang="less" scoped>

</style>