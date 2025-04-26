<template>
	<div class="box">
		<h1>组件间通信: attrs</h1>
		<HintButton
				title="Tip"
				content="this is content"
				@trigger="handleTrigger"
				@click="handleClick"
		></HintButton>
	</div>
</template>

<script lang="ts" setup>
// region >>> import 依赖
import HintButton from './HintButton.vue';
// endregion

// region >>> 概述注解
/*
* 1. $attrs - useAttrs() - v-bind="attrs"
*   接收绑定在组件标签上的所有属性
*   Tip: 接收除了 defineProps 、 defineEmits 接收过的数据，
*
* 2. $listeners
*   Tip: 对比 vue2 ，此属性被移除了。
*   vue3 中 attrs 可以接收绑定在组件上的事件.
*
* */
// endregion

// region >>> 定义函数
const handleClick = () => {
    console.log(">>> click")
}

const handleTrigger = () => {
    console.log(">>> handleTrigger");
}

// endregion
</script>

<style lang="less" scoped>

</style>