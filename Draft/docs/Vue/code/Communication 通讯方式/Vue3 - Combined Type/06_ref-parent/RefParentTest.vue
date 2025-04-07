<template>
	<div class="box">
		<h1>组件间通信: $ref & $parent</h1>

		<h2> Dad: {{ money }}</h2>
		<button @click="sonMoney(100)">lend son 100</button>
		<br>
		<button @click="daughterMoney(120)">lend daughter 120</button>

		<br>
		<Son ref="sonRef"/>
		<Daughter ref="daughterRef"/>
	</div>
</template>


<script lang="ts" setup>
// region >>> 注解
/*
在 vue2 中，获取到组件实例后，即可修改组件中的数据。
vue3 中，必须得到组件实例的许可，才可修改数据；
Tip: $children 被移除，而$parent 保留了。

由于 setup 中不存在 this, $parent 不能在 JS 部分使用。在模板中仍可使用，通过传参传给回调。
*/
// endregion

// region >>> import 依赖
import {ref} from 'vue';
import Son from './Son.vue';
import Daughter from './Daughter.vue';
// endregion

// region >>> 相关数据
const money = ref(1000);

// Ref 标识
const sonRef = ref();
const daughterRef = ref();


// endregion

// region >>> 定义函数
const sonMoney = (num: number) => {
    money.value += num;
    sonRef.value.money -= num;
}

const daughterMoney = (num: number) => {
    money.value += num;
    daughterRef.value.money -= num;
}

// endregion


</script>

