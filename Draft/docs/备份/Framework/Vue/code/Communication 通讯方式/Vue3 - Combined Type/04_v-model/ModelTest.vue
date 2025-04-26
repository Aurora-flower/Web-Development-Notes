<template>
	<div class="box">
		<h1>组件间通信: v-model</h1>
		<h3> 显示区域:</h3>
		<div> str: {{ str || "null" }}</div>
		<div> modelValue: {{ modelValue || "null" }}</div>
		<hr>

		<h3> 输入框: </h3>
		<!--	组件上的 v-model 实现-->
		<custom-input :str="str" @update:str="changeStr"></custom-input>
		<!--
		v-model 的实现:  :xxx & @update:xxx
				内部实现 - @input - emits(defineEmits)
		-->
		<custom-input_one v-model="modelValue"></custom-input_one>
		<!--
		对比 vue2:
			.sync 修饰符被移除；（v-model - .sync 合并）
			v-model 可以在组件中使用多个；
		-->
		<custom-input_two v-model="modelValue" v-model:str="str"></custom-input_two>
	</div>
</template>

<script lang="ts" setup>
// region >>> 依赖
import {ref} from "vue";
import CustomInput from './CustomInput.vue';
import CustomInput_one from './CustomInput_one.vue';
import CustomInput_two from './CustomInput_two.vue';
// endregion


// region >>> 相关数据
let str = ref<string>("");
let modelValue = ref<string>("");

// endregion

// region >>> 定义函数
const changeStr = (value: string) => {
    str.value = value;
    console.log(">>> changeNum", value);
};
// endregion

</script>
