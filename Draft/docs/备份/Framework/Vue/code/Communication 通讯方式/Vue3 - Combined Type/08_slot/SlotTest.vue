<template>
	<div class="box">
		<!-- 插槽、具名插槽、作用域插槽 -->
		<h1>组件间通信: Slot</h1>

		<h3>显示TODO列表时, 已完成的TODO为绿色</h3>
		<List :list="todos">
			<template #default="{row, $index}">
				<p :class="{green: row?.isComplete }">{{ row?.text }}</p>
			</template>
		</List>

	</div>
</template>

<script lang="ts" setup>
import {ref} from 'vue';
import type {Users} from './types';
import List from './List.vue';

const todos = ref<Users>([
    {id: 1, text: 'A', isComplete: false},
    {id: 2, text: 'B', isComplete: true},
    {id: 3, text: 'C', isComplete: false},
    {id: 4, text: 'D', isComplete: false},
])
</script>

<style lang="less" scoped>
.green {
	color: #55bb8a;
}
</style>
