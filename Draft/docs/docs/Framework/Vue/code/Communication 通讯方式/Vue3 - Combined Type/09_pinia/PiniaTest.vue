<template>
	<div class="box">
		<h1>组件间通信: Pinia</h1>
		<div>Count: {{ TestStore.count }}</div>
		<button class="ml-10" @click="addHandle">增加</button>
		<button class="ml-10" @click="subHandle">减少</button>
		<button class="ml-10" @click="test">测试</button>
	</div>
</template>

<script lang="ts">
export default {
    name: "PiniaTest"
}
</script>

<script setup lang="ts">
import {storeToRefs} from "pinia";
import {onUpdated, watch} from "vue";
import {useTestWithout} from "@/pages/09_pinia";

// PINIA
const TestStore = useTestWithout();
const { count } = storeToRefs(TestStore)
console.log(">>> TestStore:", TestStore);


// 定义函数
const addHandle = () => {
    TestStore.Increase();
};
const subHandle = () => {
    TestStore.Decrease();
};

const test = () => {
  count.value++
}

onUpdated(()=>{
  console.log('0-------')
})

// watch
</script>

<style scoped>
.ml-10 {
	margin-left: 10px;
}
</style>