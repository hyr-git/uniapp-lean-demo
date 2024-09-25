<template>
	<view class="layout">
		    <view class="stuName">{{stu.stuName}}</view>
			<image class="stuImg" :src="stu.stuImg" mode=""></image> 
	</view>
</template>

<script setup>
	defineProps({
		stu:{
			type:Object,
			default(){
				return {stuName:'匿名',stuImg:'../../static/c1.png'}
			}
		}
	})
</script>

<style>
 .layout{
		width: 100%;
        height: 250px;
		padding-top: 10px;
		padding-bottom: 10px;
		align-items: center;
		align-content: center;
		justify-content: center;
		display: flex;
		flex-direction: column;
		.stuName{
		   
		}
		.stuImag{
			width: 100px;
			height: 40px;
		}
	}
</style>