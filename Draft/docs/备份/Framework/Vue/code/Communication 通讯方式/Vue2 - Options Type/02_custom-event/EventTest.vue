<template>
  <div class="box">
    <h3>关于标签</h3>
    <!-- 系统内置的事件类型 -->
    <h4>绑定原生事件</h4>
    <!-- 由浏览器触发的 -->
    <div>count: {{ count }}</div>
    <button @click="change"> change count</button>
    <button @click="change(5, $event)"> change count two</button>
    <button @click="change($event, 6)"> change count three</button>

    <!--自己定义的事件类型-->
    <h4>绑定自定义事件</h4>
    <!--标签上的自定义事件无法触发， 且标签的绑定自定义事件无任何意义 -->
    <button @custom="change"> Custom events</button>


    <!---------------------------------------------------->
    <hr>
    <h3>关于组件</h3>
    <h4>绑定原生事件</h4>
    <!-- 在组件上绑定原生事件会被理解成自定义事件，需要通过 $emit 触发 -->
    <!--<Event_One @click="clickHandler"></Event_One>-->

    <!-- .native 修饰符：对于组件，用于监听原生事件，而不是组件内部使用 $emit 触发的事件-->
    <Event_One @click.native="clickHandler"></Event_One>

    <h4>绑定自定义事件</h4>
    <!--<Event_Two @trigger="clickHandler"></Event_Two>-->
    <!--<Event_Two @trigger="clickHandler(20)"></Event_Two>-->

    <!--此处的 $event，可以理解为一个形参，接收 $emit 触发时传递的参数 -->
    <Event_Two @trigger="clickHandler(10, $event)"></Event_Two>


    <!---------------------------------------------------->
    <hr>
    <h3> 关于参数 </h3>
    <div class="event-handler">
      <!-- Tip： 底层 fns 处理传递的回调，fns 作为真正被调用的回调 -->
      <button @click="contextHandler_One">情景 1</button>
      <!--
      ƒ contextHandler_One(e){
      console.log(">>> 情景1: 普通事件，且无参数的情况", e);
      }
      -->

      <button @click="contextHandler_Two('arg')">情景 2</button>
      <!-- ƒ ($event){return contextHandler_Two('arg')} -->

      <button @click="contextHandler_Three($event, 'arg')">情景 3</button>
      <!-- ƒ ($event){return contextHandler_Three($event, 'arg')} -->

      <button @click="this.contextHandler_Four">情景 4</button>
      <!--
      ƒ contextHandler_Four(e){
      console.log(">>> 情景4: (情景 1)回调函数加 this 的情况", e, this);
      }
      -->

      <button @click="this.contextHandler_Five('arg')">情景 5 (error)</button>
      <!-- ƒ ($event){return this.contextHandler_Five('arg')} -->

      <button @click="this.contextHandler_Six($event, 'arg')">情景 6 (error)</button>
      <!-- ƒ ($event){return this.contextHandler_Six($event, 'arg')} -->

      <!--
      结论: 绑定事件时，传递参数的情况下，底层 fns 也会包裹事件回调函数，形参为 $event 事件对象;
      为传递参数时，直接将事件回调函数的地址传递给底层 fns;
      -->
    </div>
  </div>
</template>

<script>
import Event_One from "@/pages/02_custom-event/Event_One.vue";
import Event_Two from "@/pages/02_custom-event/Event_Two.vue";

export default {
  name: "EventTest",
  data() {
    return {
      count: 1,
    }
  },
  methods: {
    contextHandler_One(e) {
      // 无括号包裹参数的情况，参数默认为事件对象;
      // 括号包裹参数的情况，底层逻辑包裹了一层，形参为 $event
      console.log(">>> 情景1: 普通事件，且无参数的情况", e);
    },
    contextHandler_Two(arg) {
      console.log(">>> 情景2: 事件传递参数的情况", arg);
    },
    contextHandler_Three(e, arg) {
      console.log(">>> 情景3: 参数包含事件对象与参数", e, arg);
    },
    contextHandler_Four(e) {
      console.log(">>> 情景4: (情景 1)回调函数加 this 的情况", e, this);
    },
    // Tip: 情景 5 报错
    contextHandler_Five(arg) {
      console.log(">>> 情景5: (情景 2)回调函数加 this 的情况", arg);
    },
    contextHandler_Six(e, arg) {
      console.log(">>> 情景6: (情景 3)回调函数加 this 的情况", e, arg);
    },
    change(e, arg) {
      this.count++;
      // console.log(this); // 指向当前活跃的组件实例
      console.log(e); // 默认接收一个事件对象参数
      console.log(arg);
    },
    clickHandler(arg_one, arg_two) {
      console.log(">>> 触发原生事件", arg_one, arg_two);
    },
  },
  components: {
    Event_One,
    Event_Two,
  }
}
</script>

<style scoped>

</style>