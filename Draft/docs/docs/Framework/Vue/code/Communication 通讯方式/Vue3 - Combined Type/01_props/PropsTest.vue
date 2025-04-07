<template>
	<div class="box">
		<h1>组件间通信: props</h1>

		<!-- region >>> 父组件 -->
		<h2>Father</h2>
		<div> Message: {{ message }}</div>
		<div> Data_Name: {{ data.name }}</div>
		<button @click="changeData">change</button>
		<!-- endregion -->

		<hr>

		<!-- region >>> 子组件 -->
		<h2>Child</h2>
		<!--
    非函数：基础类型或引用类型；
    函数：主要用于修改数据；
    -->
		<!-- vue 支持 “-” 连接，替代小驼峰式写法    -->
		<Child :message="message" :data="data"
			   :change-msg="changeMsg"
			   :change-data="changeData">
		</Child>

		<!-- endregion -->

	</div>
</template>

<script lang="ts" setup>
// region >>> 相关依赖
import {ref} from "vue";
import Child from "@/pages/01_props/Child.vue";
// endregion

// region >>> 定义数据
let message = ref("message");
let data = ref({name: "king"}); // 对象使用 ref 或 reactive
// let data = reactive({name: "huayin"});
// endregion

// region >>> 定义函数

// 改变基本数据类型
const changeMsg = (e?: InputEvent) => {
    // 解决 target 飘红： 类型断言
    message.value = (e?.target as HTMLInputElement).value;
}

// 改变引用数据类型
const changeData = () => {
    data.value.name += "HuaYin";

		// 使用 reactive 包裹对象时，数据更新，但地址更改；数据不被显示；
    // data.name += "HuaYin";
}
// endregion

</script>
