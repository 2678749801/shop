<template>
	<view>
		<view class="goods-list">
			<view class="goods-item" v-for="item in goods" :key="item.id" @click="navigator(item.id)">
				<image src="//m.360buyimg.com/mobilecms/s750x750_jfs/t1/143051/26/15747/73035/5fbdd54cE80757a48/67c387e1d0dc5c83.jpg!q80.dpg.webp" mode=""></image>
				<view class="price">
					<text>￥{{item.sell_price}}</text>
					<text>￥{{item.market_price}}</text>
				</view>
				<view class="name">{{item.title}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"goods-list",
		props:['goods'],
		data() {
			return {
				
			};
			
		},
		methods:{
			navigator(id){
				this.$emit('goodItemClick',id)
			}
		}
	}
</script>

<style lang="scss">
.goods-list{
	padding: 0 15rpx;
	display: flex;
	flex-wrap: wrap;
	justify-content: space-between;
	.goods-item{
		background: #fff;
		width: 355rpx;
		margin:10rpx 0;
		padding: 15rpx;
		box-sizing: border-box;
		image{
			width: 80%;
			height: 150px;
			display: block;
			margin: auto;
		}
		.price{
			color: #b50e03;
			font-size: 36rpx;
			text:nth-child(2){
				color:#ccc;
				font-size: 28rpx;
				margin-left: 7rpx;
				text-decoration: line-through;
			}
		}
		.name{
			font-size: 32rpx;
			line-height: 50rpx;
			padding-bottom: 15rpx;
			padding-top: 10rpx;
		}
	}
				}
</style>
