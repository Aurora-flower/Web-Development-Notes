<template>
	<div class="box">
		<h1>组件间通信: provide & inject</h1>
		<Child></Child>
	</div>
</template>

<script lang="ts" setup>
/**
 * 1. provide（提供） & inject（注入）
 *    用于祖孙之间的通信，需要从 vue 中引入，同样只是在初始化的时候传递一次。
 *
 * 2. 不同于 vue2，vue3 中后代可以监听到组先的数据变化，
 *  因为 vue3 中的响应需要 ref 包裹，修改的是 ref 对象下的 value 属性。
 * */
import {ref, provide} from "vue";
import Child from './Child.vue';

// 定义 value
interface ObjectModel {
    name: string,
    age: number
}

const content = ref<string>("content"); // 基本数据类型
const obj = ref<ObjectModel>({name: "HuaYin", age: 20}); // 引用数据类型
const changeHandle = () => {
    (obj.value as ObjectModel).name = "花楹一间";
    console.log(">>> changeHandle");
};

// key -value
provide("obj", obj);
provide("content", content);
provide("changeHandle", changeHandle);
</script>
