<template>
	<view class="goods-detail">
		<swiper indicator-dots>
			<swiper-item>
				<image src="https://img2.baidu.com/it/u=1369469582,3256973191&fm=26&fmt=auto&gp=0.jpg" mode=""></image>
			</swiper-item>
			<swiper-item>
				<image src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fgss0.baidu.com%2F-fo3dSag_xI4khGko9WTAnF6hhy%2Fzhidao%2Fpic%2Fitem%2Fa71ea8d3fd1f4134b1ddb26d291f95cad1c85e3e.jpg&refer=http%3A%2F%2Fgss0.baidu.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1619671092&t=61c05eabfb64d2346b624b4ef7f78630"></image>
			</swiper-item>
		</swiper>
		<view class="box1">
			<view class="price">
				<text>{{info.sell_price}}</text>
				<text>{{info.market_price}}</text>
			</view>
			<view class="goods-name">{{info.title}}</view>
		</view>
		<view class="line"></view>
		<view class="box2">
			<view>货号{{info.goods_no}}</view>
			<view>库存{{info.stock_quantity}}</view>
		</view>
		<view class="line"></view>
		<view class="box3">
			<view class="title">详情接受</view>
			<view class="content">
				<rich-text :nodes="content"></rich-text>
			</view>
		</view>
		<view class="goods-nav">
			<uni-goods-nav :fill="true"  :options="options" :buttonGroup="buttonGroup"  @click="onClick" @buttonClick="buttonClick" />
		</view>
		
	</view>
</template>

<script>
import uniGoodsNav from '@/uni_modules/uni-goods-nav/components/uni-goods-nav/uni-goods-nav.vue'
	export default {
		components:{
			uniGoodsNav,
		},
		data() {
			return {
				id:0,
				info:{},
				content:'',
				 options: [
					 {
								icon: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/uni/goodsnav/kefu.png',
								text: '客服'
						}, {
								icon: 'shop',
								text: '店铺',
								info: 2,
								infoBackgroundColor:'#007aff',
								infoColor:"red"
						}, {
								icon: 'cart',
								text: '购物车',
								info: 2
						}],
						buttonGroup: [{
							text: '加入购物车',
							backgroundColor: '#ff0000',
							color: '#fff'
						},
						{
							text: '立即购买',
							backgroundColor: '#ffa200',
							color: '#fff'
						}
						]
			}
		},
		methods: {
			 onClick (e) {
			        uni.showToast({
			          title: `点击${e.content.text}`,
			          icon: 'none'
			        })
			      },
			      buttonClick (e) {
			        console.log(e)
			        this.options[2].info++
			      },
			// getSwiper(){
			// 	this.$myRequest({
			// 		url:'/api/getthumimage/'+this.id
			// 	})
			// 	console.log(res);
			// }
		 getDetailInfo(){
				this.$myRequest({
					url:'/api/goods/getinfo/'+this.id
				}).then(res=>{
						this.info=res.data.message[0]
				})
			},
			getDetailContent(){
				this.$myRequest({
					url:'/api/goods/getdesc/'+this.id
				}).then(res=>{
					 this.content=res.data.message[0].content
				})
			}
		},
		onLoad(options) {
			this.id=options.id
			this.getDetailInfo()
			this.getDetailContent()
		}
	}
</script>

<style lang="scss">
.goods-detail{
	swiper{
		height: 700rpx;
		image{
			width: 100%;
		}
	}
	.box1{
		padding: 10px;
		.price{
			font-size: 35rpx;
			color:red;
			line-height: 80rpx;
			text:nth-child(2){
				color:#ccc;
				font-size: 28rpx;
				text-decoration: line-through;
				margin-left: 20rpx;
			}
		}
		.goods-name{
			font-size: 32rpx;
			line-height: 60rpx;
		}
	}
	.box2{
		padding: 0 10rpx;
		font-size: 32rpx;
		line-height: 60rpx;
	}
	.box3{
		.title{
			font-size: 30rpx;
			padding-left: 10px;
			border-bottom: 1px solid #eee;
			line-height: 70rpx;
		}
		.content{
			padding: 10px;
			font-size: 28rpx;
			color: #333;
			line-height: 50rpx;
			
		}
	}
}
.goods-nav{
	position: fixed;
	bottom: 0;
	width: 100%;
}
.line{
	height: 15rpx;
	width: 750rpx;
	background: #eee;
}

</style>
