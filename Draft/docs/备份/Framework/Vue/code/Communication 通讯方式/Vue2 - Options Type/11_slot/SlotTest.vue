<template>
  <div class="box">
    <!-- 默认插槽，具名插槽，作用域插槽-->

    <!-- v-slot:default 简写 #default -->
    <!--<List :list="todos">-->
    <!--  <template #default="{text, isComplete}">-->
    <!--    <div :class="{hint: isComplete}">-->
    <!--      {{ text }}-->
    <!--    </div>-->
    <!--  </template>-->
    <!--</List>-->


    <!--
    v-slot:slot_name="{}"
    接收一个变量，包含 slot 插槽上所有的属性和属性值，是一个对象数据类型;
    -->
    <List :list="todos">
      <template v-slot:show="{text, isComplete}">
        <div :class="{hint: isComplete}">
          {{ text }}
        </div>
      </template>
    </List>

  </div>
</template>

<script type="text/ecmascript-6">
import List from './List.vue'

export default {
  name: 'SlotTest',
  data() {
    return {
      todos: [
        {id: 1, text: 'A - 含辞未吐，气若幽兰。华容婀娜，令我忘餐。', isComplete: false},
        {id: 2, text: 'B - 我见青山多妩媚，料青山见我应如是。', isComplete: true},
        {id: 3, text: 'C - 世人谓我恋长安，其实只恋长安某。', isComplete: false},
        {
          id: 4, text: 'D - 如果能避开猛烈的狂喜，自然不会有悲痛的来袭。\
              可是他自人山人海而来，这猛烈的欢喜，我避之不及，甘之如饴。', isComplete: false
        },
      ]
    }
  },
  components: {
    List
  }
}
</script>

<style>
li {
  list-style: none;
}

.hint {
  color: #418688;
}
</style>
