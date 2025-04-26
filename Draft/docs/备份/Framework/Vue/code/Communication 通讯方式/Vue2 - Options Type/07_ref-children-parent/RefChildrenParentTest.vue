<template>
  <div class="box">
    <h3> Dad: {{ money }}</h3>
    <button @click="borrowMoneySon(200)">Borrowing son:200</button>
    <button @click="borrowMoneyDaughter(100)">Borrowing daughter:100</button>
    <button @click="borrowMoneyAll(200)">Borrowing All:200</button>

    <hr>
    <br/>
    <Son ref="son"/>

    <br/>
    <Daughter ref="daughter"/>
  </div>
</template>

<script>
import Son from "./Son.vue";
import Daughter from "./Daughter.vue";

export default {
  name: "RefChildrenParentTest",
  data() {
    return {
      money: 1000,
    };
  },
  components: {
    Son,
    Daughter,
  },
  // 在 Vue.js 中，可以通过 ref 引用来获取到子组件实例，并直接操作它的数据。
  methods: {
    borrowMoneySon(num) {
      // $refs 用于获取到组件实例（区别于之前只用来获取 DOM 元素）
      if (this.$refs.son.money - num < 0) {
        return;
      }
      this.money += num;
      this.$refs.son.money -= num;
    },
    borrowMoneyDaughter(num) {
      if (this.$refs.daughter.money - num < 0) {
        return;
      }
      this.money += num;
      this.$refs.daughter.money -= num;
    },
    borrowMoneyAll(num) {
      if (this.$refs.son.money - num < 0
          || this.$refs.daughter.money - num < 0) {
        return;
      }
      this.money += num;

      // 原写法
      // this.$refs.son.money -= num;
      // this.$refs.daughter.money -= num;

      // $children 用于获取到当前组件中的子组件，得到的是一个数组；
      this.$children.forEach(item => item.money -= num);

    },
  }
};
</script>

<style>
</style>
