<template>
		
	<view class="container">
		
		<pet-comp :petArs="stuList"></pet-comp>
		
		
		<view class="intro">本项目已包含uni ui组件，无需import和注册，可直接使用。在代码区键入字母u，即可通过代码助手列出所有可用组件。光标置于组件名称处按F1，即可查看组件文档。</view>
		<text class="intro">详见：</text>
		<uni-link :href="href" :text="href"></uni-link>
		<view class="info">
			shskhshshshsh
		
		</view>
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
		{stuName:'李戚薇',stuImg:'../../static/c5.png',age:63},
		{stuName:'232323',stuImg:'../../static/c5.png',age:63}
	]);
</script>

<style>
	.container {
		padding: 20px;
		font-size: 14px;
		line-height: 24px;
	}
</style>
