<template>
  <div class="box">
    <h3>GrandFather</h3>
    <h4> 展示区域 </h4>
    <div> Text: {{text}}</div>
    <div> Content: {{content.name}}</div>

    <hr>
    <Child></Child>
  </div>
</template>

<script>
import Child from "@/pages/09_provide-inject/Child.vue";

// provide-inject 用于祖孙之间的通信
/*
Tip: 数据只会传输一次，后续数据的更新，不会触发再次传递;
（此时，与祖组件的传递的对象不是一个地址）;
*/
export default {
  name: "ProvideInjectTest",
  components: {
    Child,
  },
  // provide 是一个钩子函数,用于 return 抛出数据
  provide() {
    return {
      content: this.content,
      text: this.text,
    }
  },
  data() {
    return {
      text: "This is a joke.",
      content: {
        name: "Tom and Jamie",
      },
    };
  },
  mounted() {
    // 证明：数据只会传递一次
    setInterval(()=>{
      this.changeData()
    }, 1500);

    // 对象在不改变地址的情况下，改变数据，会传递给子组件；
    setInterval(()=>{
      this.changeObj()
    }, 1500)
  },
  methods: {
    changeData(){
      this.text += "Jan";
    },
    changeObj(){
      // 当改变对象属性数据时，可以接收显示，是由于这个对象的地址没有变。
      this.content.name += "JoJo";

      // 向后代传递对象的时候，当地址改变时，后代无法接收到数据；
      // this.content = {
      //   name: "huayin"
      // }
    },
  }
};
</script>

<style lang="less" scoped>
</style>
