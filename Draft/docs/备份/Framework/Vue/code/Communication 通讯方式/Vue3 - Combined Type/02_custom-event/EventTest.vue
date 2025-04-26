<template>
	<div class="box">
		<h1>组件间通信: 自定义事件</h1>
		<!-- 绑定原生事件 -->
		<!--
			无根标签包裹的情况或被 defineEmits 接收的事件，都被解析为自定义事件
		-->
		<Event_One @click="nativeHandler"></Event_One>

		<!-- 绑定自定义事件 -->
		<Event_Two @trigger="triggerHandler"></Event_Two>
	</div>
</template>

<script lang="ts" setup>
import Event_One from './Event_One.vue';
import Event_Two from './Event_Two.vue';

// region >>> 相关注解
/**
 * 相比较 vue2:
 *  组件上绑定原生事件，不会再被解析为自定义事件，即意味着 .native 修饰符被移除;
 *
 * 条件:
 *   必须是绑定在组件的根标签上，若是无唯一根标签包裹，则被解析为自定义事件，需要手动触发；
 *
 * 自定义事件的触发：
 *   defineEmits() —— 接收自定义事件名称，返回一个 emits 函数，由此函数触发事件;
 * */
// endregion

// region >>> 定义函数 - 事件回调
const nativeHandler = (arg?: any) => {
    console.log(">>> nativeHandler", arg);
};

const triggerHandler = () => {
    console.log(">>> triggerHandler")
}
// endregion

</script>
