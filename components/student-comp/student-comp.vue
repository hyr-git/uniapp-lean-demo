<template>
	<view class="layout">
		    <view class="stuName">{{studentProps.studentName}}</view>
			<image class="stuImg" :src="studentProps.studentImage" mode=""></image> 
			
	</view>
</template>

<script setup>
 /* const props = defineProps(['stuName','stuImg'])
  console.log(props.stuImg)
  const studentName = props.stuName+"@" 
  console.log(studentName) */
  
  const studentProps = defineProps({
	  studentName:{
		  type:String,
		  default:'匿名'
	  },
	  studentImage:{
		  type:String,
		  default:'../../static/c1.png'
	  },
	  age : Number
  })
  console.log(studentProps)
  
</script>

<style scoped>
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