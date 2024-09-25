<template>
	<view class="container">
		<view class="layout">
          <view class="box" v-for="(item,index) in petArs">
			  <view class="pic">
				  <!-- //图片变形， mode="widthFix"设置以宽度为基准高度自动延伸 -->
				  <image :src="item.stuImg" mode="widthFix"></image>
			  </view>
			  <view class="text">{{item.stuName}}</view>
		  </view>
		</view>  
	</view>
</template>

<script setup>
  defineProps({
	   petArs:{
		   type: Array,
		   default:()=>[{
			   stuImg:String,
			   stuName:String
		   }]
	   }
   });
</script>

<style lang="scss" scoped>
	.container{
		.layout{
			padding: 50rpx;//控制元素所有四条边的内边距区域,平均每25。
			.box{
				margin-bottom: 60rpx;//设置盒子的边距
				//设置盒子边框的阴影效果，该属性可设置的值包括阴影的 X 轴偏移量、Y 轴偏移量、模糊半径、扩散半径和颜色。
				box-shadow: 0 10rpx 40rpx rgba(0, 0, 0,0.08);
				border-radius: 10rpx;//允许你设置元素的外边框圆角
				overflow: hidden;
				.pic{
					image{
						width: 100%;
					}
				}
				.text{
					padding: 30rpx;
					color:#333;
				    font-size: 36rpx;
				}
				.author{
					padding: 0 30rpx 30rpx;
					color:#888;
					font-size: 28rpx;
					text-align: right;
				}
			}
		}
	}
	
</style>