<template>
	<view>
		<stu-comp v-for="(item,index) in stuList" :stu='item'></stu-comp>
	</view>
</template>

<script setup>
import { ref } from 'vue';
	const stuList = ref([
		{stuName:'李凯峰',stuImg:'../../static/c1.png',age:23},
		{stuName:'张容器',stuImg:'../../static/c2.png',age:33},
		{stuName:'唐丽君',stuImg:'../../static/c3.png',age:43},
		{stuName:'奏凯',stuImg:'../../static/c4.png',age:53},
		{stuName:'李戚薇',stuImg:'../../static/c5.png',age:63},
		{stuImg:'../../static/c5.png',age:63},
		{stuName:'',stuImg:null,age:63}
	])
</script>

<style>

</style>
