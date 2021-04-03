<template>
	<view class="pics">
		<scroll-view class="left" scroll-y>
			<view 
			:class="active===index?'active':''" 
			v-for="(item,index) in cates" 
			:key="index"
			@click="leftClick(index,item.id)"
			>{{item.title}}</view>
			
		</scroll-view>
		<scroll-view class="right" scroll-y>
			<view class="item" v-for="item in secondData" :key="item.id">
				<image @click="previewImg(item.img_url)" src="https://img2.baidu.com/it/u=3319438021,2309257658&fm=26&fmt=auto&gp=0.jpg"></image>
			<!-- 	<image :src="item.img_url"></image> -->
				<text>{{item.title}}</text>
			</view>
			<text v-if="secondData.length===0">暂无数据</text>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cates:[],
				active:5,
				secondData:[],
			}
		},
		onLoad() {
			this.getPicsCate()
		},
		methods: {
			async getPicsCate(){
				const res= await this.$myRequest({
					url:'/api/getimgcategory'
				})
				this.cates=res.data.message
				this.leftClick(0,this.cates[0].id)
			},
			async leftClick(index,id){
				this.active=index
				const res = await this.$myRequest({
					url:'/api/getimages/'+id
				})
				this.secondData = res.data.message
			},
			previewImg(current){
				const urls= this.secondData.map(item=>{
					return item.img_url
				})
				uni.previewImage({
					current,
					urls,
				})
			}
		}
	}
</script>

<style lang="scss">
	page{
		height: 100%;
	}
.pics{
	height: 100%;
	display: flex;
	.left{
		width: 200rpx;
		height: 100%;
		border-right: 1px solid #eee;
		view{
			height: 60px;
			line-height: 60px;
			color:#333;
			text-align: center;
			font-size: 30rpx;
			border-top:1px solid #eee;
		}
		.active{
		background: #b50e03;
		color: #fff;
		}
	}
	.right{
		height: 100%;
		width: 520rpx;
		margin: 0 auto;
		.item{
			image{
				width: 520rpx;
				height: 520rpx;
				border-radius: 5px;
			}
			text{
				font-size: 30rpx;
				line-height: 60rpx;
			}
		}
	}
}
</style>
