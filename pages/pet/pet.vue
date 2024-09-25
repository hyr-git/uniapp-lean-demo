<template>
	<view class="container">
		 <view>
			<uni-segmented-control :current="current" :values="itemValues" @clickItem="onClickItem" 
			styleType="button" activeColor="#4cd964"></uni-segmented-control>
		</view>
		
		<view class="layout">
			<view class="box" v-for="(item,index) in pets" :key="item.id">
				<view class="pic">
					<!-- //图片变形， mode="widthFix"设置以宽度为基准高度自动延伸 -->
					<image :src="item.url" lazy-load mode="widthFix" @click="showImge(index)"></image>
				</view>
				<view class="text">{{item.content}}</view>
				<view class="author">----{{item.author}}</view>
			</view>
		</view>

		<view class="float">
			<view class="item" @click="onRefresh"> 刷新 </view>
			<view class="item" @click="onUpTopPage"> 置顶 </view>
		</view>
		
		<view class="loadMore">
			<uni-load-more :status="status" @clickLoadMore="clickLoadMore"></uni-load-more>
		</view>
	</view>
</template>

<script setup>
	
	/***
	 * 通过list集合模拟数据
	 * type = all -全部,travel -旅游,beauty -美女,delicacy -美食
	 * 
	 *
	 *
	 * 
	 * 
	 * *****/
	
	
	
	import {ref} from 'vue';
	import {onReachBottom,onPullDownRefresh} from "@dcloudio/uni-app"
	let pageSize = 5;
	let currentPageNum = 1;
	const status = ref('loading');
	const personList = ref([
		{id:"1",author:'李凯峰',url:'../../common/image/beauty/001.jpg',type:'beauty',content:"你想去哪儿旅游",age:23},
		{id:"2",author:'张容器',url:'../../common/image/travel/002.jpg',type:'travel',content:"去哪儿旅游还没有想好的话，可以考虑来体验西北的风情",age:33},
		{id:"3",author:'唐丽君',url:'../../common/image/travel/003.jpg',type:'travel',content:"去哪儿旅游有什么推荐的住宿地方吗?",age:43},
		{id:"4",author:'奏凯',url:'../../common/image/beauty/004.jpg',type:'beauty',content:"去哪儿旅游",age:53},
		{id:"5",author:'李戚薇',url:'../../common/image/beauty/005.jpg',type:'beauty',content:"去哪儿旅游",age:63},
		{id:"6",author:'牛群',url:'../../common/image/beauty/006.jpg',type:'beauty',content:"去哪儿旅游",age:63},
		{id:"7",author:'牛莉',url:'../../common/image/beauty/007.jpg',type:'beauty',content:"去哪儿旅游",age:63},
		{id:"8",author:'曹珊珊',url:'../../common/image/travel/008.jpg',type:'travel',content:"去哪儿旅游",age:63},
		{id:"9",author:'李云龙',url:'../../common/image/delicacy/005.jpg',type:'delicacy',content:"去哪儿旅游",age:63},
		{id:"10",author:'赵甜甜',url:'../../common/image/delicacy/006.jpg',type:'delicacy',content:"去哪儿旅游",age:63},
		{id:"11",author:'张坤',url:'../../common/image/delicacy/001.jpg',type:'delicacy',content:"去哪儿旅游",age:63},
		{id:"12",author:'林坤',url:'../../common/image/delicacy/002.jpg',type:'delicacy',content:"去哪儿旅游",age:63},
		{id:"13",author:'古雄',url:'../../common/image/delicacy/003.jpg',type:'delicacy',content:"去哪儿旅游",age:63},
		{id:"14",author:'李处',url:'../../common/image/travel/014.jpg',type:'travel',content:"去哪儿旅游",age:63},
		{id:"15",author:'李一舟',url:'../../common/image/travel/015.jpg',type:'travel',content:"去哪儿旅游",age:63},
		{id:"16",author:'宋巧梅',url:'../../common/image/travel/016.jpg',type:'travel',content:"去哪儿旅游",age:63},
		{id:"17",author:'找一天',url:'../../common/image/travel/017.jpg',type:'travel',content:"去哪儿旅游",age:63},
		{id:"18",author:'冯军磊',url:'../../common/image/travel/018.jpg',type:'travel',content:"去哪儿旅游",age:63},
		{id:"19",author:'凯泽汇',url:'../../common/image/travel/019.jpg',type:'travel',content:"去哪儿旅游",age:63},
		{id:"20",author:'胡军林',url:'../../common/image/travel/020.jpg',type:'travel',content:"去哪儿旅游",age:63}
	]);

	const pets = ref([]);

	/***
	 *第一页数据  0-4,第二页数据5-9
	 * 
	 * 
	 */
	function findPerson(pageNo) {

		if (pageNo && pageNo > 0 && pageNo <= 4) { //返回指定页码的值
			return pets.value = personList.value.slice((pageNo - 1) * pageSize, (pageNo) * pageSize);
		} else {
			return pets.value = personList.value.slice(0, pageSize);
		}
	}

	//onLoad中调用
	findPerson(1);




	/**
	 * 图片放大预览
	 * @param {Object} index
	 */
	const showImge = function(index) {
		let petUrls = personList.value.map(item => item.url);
		uni.previewImage({
			current: index,
			urls: petUrls
		})
	};

	/* const uni.startPullDownRefresh({
		success: res => {},
		fail: () => {},
		complete: () => {}
	}); */

	/***
	 * 点击刷新
	 */
	function onRefresh() {
		uni.startPullDownRefresh();
	}


    /***
	 * 触底刷新功能
	 */ 
	onReachBottom((e)=>{
		console.log("onReachBottom-------------"+e)
		//uni.startPullDownRefresh();
		if (personList.value.length / pageSize > currentPageNum) {
			status.value='loading'
			currentPageNum++;
		} else {
			uni.showToast({
				title: '没有最新的内容了...',
				duration: 2000
			});
			
			//noMore
			status.value='noMare'
			return;
		}
		let petOlds = pets.value;
		let petNews = findPerson(currentPageNum);
		pets.value = [...petOlds,...petNews];
		setTimeout(function() {
			uni.stopPullDownRefresh();
		}, 500);
	});
	 
    

    /****
	 * 下来刷新操作
	 */ 
	onPullDownRefresh(() => {
		console.log('--------------onPullDownRefresh');
		if (personList.value.length / pageSize > currentPageNum) {
			currentPageNum++;
			let petOlds = pets.value;
			let petNews = findPerson(currentPageNum);
			pets.value = [...petNews, ...petOlds];
			onUpTopPage();
			setTimeout(function() {
				uni.stopPullDownRefresh();
			}, 500);	
		} else {
			uni.showToast({
				title: '没有最新的内容了...',
				duration: 2000
			});
            setTimeout(function() {
				uni.stopPullDownRefresh();
		    }, 500);			
		
		    return;
		}
	})
	

	/***
	 * 置顶处理
	 */
	const onUpTopPage = function() {
		console.log('--------------onUpTOp');
		uni.pageScrollTo({
			scrollTop: 0,
			duration: 100
		})
	}

	/* uni.onPullDownRefresh () {
			console.log('refresh');
			setTimeout(function () {
				uni.stopPullDownRefresh();
			}, 1000); 
		}
	 */
	/* 
		
		function network(){
			uni.request({
				url:"https://api.thecatapi.com/v1/images/search",
				data:{
					limit:10
				}
			}).then(res=>{
				//TODO 返回结果状态判断以及异常信息提示
				pets.value=res.data;
				console.log("--------then"+pets.value);
				
			}).catch(res=>{
				console.log("catch-------"+res);
			})
		    .finally(res=>{
				console.log("finally-------"+res);
			})
	    };
		
		network(); */

	/*** 
	   3、刷新、
	   安全触底边框
	  5、扩展组件6、加载更多提示
	***/
	
	
	//type = all -全部,travel -旅游,beauty -美女,delicacy -美食
	 const items = [
		 {itemcode:'all',itemName:'全部'},
		 {itemcode:'travel',itemName:'旅游'},
		 {itemcode:'beauty',itemName:'美女'},
		 {itemcode:'delicacy',itemName:'美食'},
	 ];
	 
	const itemValues = items.map(item=>item.itemName);
	 
	 const current=ref(0);
	 function onClickItem(e){
		 current.value = e.currentIndex;
		 
		 const currentType = items[current.value].itemcode;
		 
		 if(currentType==='all'){
			 pets.value = personList.value;
		 }else{
			 pets.value = personList.value.filter(item=>item.type===currentType);
		 }
	 }
</script>

<style lang="scss" scoped>
	.container {
		.layout {
			padding: 50rpx; //控制元素所有四条边的内边距区域,平均每25。

			.box {
				margin-bottom: 60rpx; //设置盒子的边距
				//设置盒子边框的阴影效果，该属性可设置的值包括阴影的 X 轴偏移量、Y 轴偏移量、模糊半径、扩散半径和颜色。
				box-shadow: 0 10rpx 40rpx rgba(0, 0, 0, 0.08);
				border-radius: 10rpx; //允许你设置元素的外边框圆角
				overflow: hidden;
				z-index: 0;

				.pic {
					image {
						width: 100%;
					}
				}

				.text {
					padding: 30rpx;
					color: #333;
					font-size: 36rpx;
				}

				.author {
					padding: 0 30rpx 30rpx;
					color: #888;
					font-size: 28rpx;
					text-align: right;
				}
			}


		}

		.float {
			position: fixed;
			right: 30rpx;
			bottom: 80rpx;
			padding-bottom: cacl(constant(safe-area-inset-bottom)+ 40 rpx);
			padding-right: 30rpx;
			color: #ccc;

			.item {
				width: 80rpx;
				height: 70rpx;
				background: rgba(255, 255, 255, 0.9);
				border-radius: 50%;

				//居中显示
				display: flex;
				align-items: center;
				justify-content: center;
				border: 1px solid #eee;
			}
		}
		
		//相对安全的位置动态增肌100rpx显示【加载更多提示信息】
		.loadMore{
			padding-bottom:calc(env(safe-area-inset-bottom) + 100rpx);
		}
	}
</style>