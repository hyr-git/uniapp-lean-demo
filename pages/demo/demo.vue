<template>
	<view id="demo">
		<view>
			<view class="stu">{{'烧过水个'}}</view>
		</view>
		------------------------------
		<view class="stuClass">
			<view class="item">
			<text>选择：</text> <text>序号</text> <text>姓名</text>
			</view>
			<checkbox-group @change="stuChange">
			<view class="item" v-for="(item,indexStu) in studentList" :key="item.id" >
				<checkbox :value="item.id+''" :checked="item.checked"></checkbox>
				<text> {{ indexStu +1}}</text>
				<text class="nameClass"> {{ item.name}}</text>
				<text class="nameClass"> {{ item.address}}</text>
				<text class="priceClass"> {{ item.price}}</text>
			    <text class='delClass' @click="delSutdentByIndex(indexStu)"> 删除</text>
			</view>
			</checkbox-group>
		</view>
		------------------------------
		
		<view class='totalShow'>
		    <checkbox-group @change="allCheckedFun">
				<checkbox :checked="allChecked" > 全选</checkbox>
			</checkbox-group>
			<view >
			      总选择了{{itemValueList.length}}用户，总价为：{{totalAccount}}元
		    </view>
		</view>
		
		
		{{itemValueList}}
		------------------------------
		{{studentList}}
	</view>
</template>

<script setup>
	import {computed, ref, watch} from "vue";
	
	
	const allChecked = ref(false);
	
	//选中的数量
	const itemValueList = ref([]);
	
	//金额总
	const totalAccount = computed(()=>{
		return studentList.value.filter(item=>item.checked).reduce((prev, cur)=>{
			return prev + cur.price;
		},0)
	});
	
	
	 
	
	const studentList = ref([
		{
			id:1,name:"王俊青",age:10,address:'陕西省宝鸡市扶风区',price:2300,checked:false
		},
		{
			id:2,name:"蔡军青",age:20,address:'陕西省宝鸡市凤翔区',price:3400,checked:false
		},
		{
			id:3,name:"柳树",age:30,address:'陕西省宝鸡市朝阳区',price:4500,checked:false
		},
		{
			id:4,name:"牛大人",age:40,address:'陕西省宝鸡市李沧区',price:5600,checked:false
		}
	]);
	
	 function stuChange(e){
		 itemValueList.value = e.detail.value;
		 //console.log(checkList.value)
		 
		/*****
		 *  使用foreach方式进行处理会修改源对象的值
		 */
		 //选中之后进行勾选操作
		/* studentList.value.forEach(item=>{
			 item.checked = itemValueList.value.includes(item.id+'')
		 }); */
		 
		/*****
		 *  使用map方式进行处理不会修改源对象的值
		 */
		studentList.value = studentList.value.map(item=>({
			...item,
			checked:itemValueList.value.includes(item.id+'')
		})); 

        /* studentList.value = studentList.value.map(function(item){ 
			return 
        	...item,
        	checked:itemValueList.value.includes(item.id+'')
        });	 */	 
		 
		let checkStudentList = studentList.value.filter(item=>item.checked);
		 console.log("选中的元素："+checkStudentList)
		 
		/* //计算总金额
		 totalAccount.value = checkStudentList.reduce(function(prev, cur){
			 return prev+cur.price
		 },0);//.map(item=>item.checked=true);
		 console.log(totalAccount.value) */
		 
		
	 }
	
	/***
	 *  删除对象
	 */
	function delSutdent(item){
		console.log("delSutdent----"+item)
		studentList.value = studentList.value.filter(cur=> cur!==item);
	}
	
	/***
	 *  通过索引删除对象
	 */
	function delSutdentByIndex(index){
		console.log("delSutdentByIndex"+index)
		studentList.value.splice(index,1);
		itemValueList.value = studentList.value.filter(item=>item.checked).map(item=>item.id)
	}
	
	const allCheckedFun = function(e){
		let selected = !allChecked.value ;
		//选中之后将所有选项变为true 
		studentList.value.forEach(item=>{
			item.checked = selected
		});
		
		itemValueList.value = selected ? studentList.value.map(item=>item.id)  : [];
		
	}
	
	
	//所有的选项选中时，将全选按钮设置为选中
	watch(studentList,()=>{
		allChecked.value = studentList.value.every(item=>item.checked) 
	},{deep:true})
	
</script>

<style lang="scss" scoped>
  .stuClass{
	  padding: 10px;
	  .item{
		  padding: 10px 0;
		  margin-left: 30px;
		  margin: 10px;
		  .delClass{
			   margin-left: 10px;
			  color:orangered;
		  }
		  .nameClass{
			  margin-left: 10px;
			  color:ccc0fd;
		  }
		  .priceClass{
			  margin-left: 10px;
			  color:red;
		  }
	  }
  }
</style>
