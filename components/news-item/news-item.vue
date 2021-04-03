<template>
	<view>
		<view class="news-item" v-for="item in list" :key="item.id" @click="navgator(item.id)">
			<!-- <image :src="item.img_url" mode=""></image> -->
			<image src="https://img0.baidu.com/it/u=1803182527,817656962&fm=26&fmt=auto&gp=0.jpg" mode=""></image>
			<view class="right">
				<view class="title">
					{{item.title}}
				</view>
				<view class="info">
					<text>发布时间{{item.add_time| formatDate}}</text>
					<text>浏览次数{{item.click}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>

	export default {
		name:"news-item",
		props:['list'],
		filters:{
			formatDate(date){
				const nDate= new Date(date)
				const year=nDate.getFullYear()
				const month=nDate.getMonth().toString().padStart(2,0)
				const day=nDate.getDay().toString().padStart(2,0)
				
				return year+'-'+month+'-'+day
			}
		},
		data() {
			return {
				
			};
		},
		methods:{
			navgator(id){
				
				this.$emit('itemClick',id)
			}
		}
	}
</script>

<style lang="scss">
.news-item{
		display: flex;
		padding: 10rpx 20rpx;
		border-bottom: 1px solid red;
		image{
			
			min-width: 200rpx;
			max-width: 200rpx;
			height: 150rpx;
		}
		.right{
			margin-left: 15rpx;
			display: flex;
			flex-direction: column;
			justify-content: space-between;
			.title{
				font-size: 30rpx;
				
			}
			.info{
				font-size: 24rpx;
				text:nth-child(2){
					margin-left:30rpx;
				}
			}
		}

	}
</style>
