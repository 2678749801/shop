<template>
	<view class="home">
		<swiper indicator-dots circular="">
			<swiper-item v-for="item in swipers " :key="item.id">
				<image :src="item.img" mode=""></image>
			</swiper-item>
		</swiper>
		<view class="nav">
			<view class="nav-item" v-for="(item,index) in navs" :key="index" @click="navItemClick(item.path)">
				<view :class="item.icon"></view>
				<text>{{item.title}}</text>
			</view>
		</view>
		<view class="hot-goods">
			<view class="title">推荐商品</view>
			<good-list :goods="goods" @goodItemClick="goGoodsDetail"></good-list>
		</view>
	</view>
</template>

<script>
	import goodList from '../../components/goods-list/goods-list.vue'
	export default {
		components:{
			goodList,
		},
		data() {
			return {
				swipers:[],
				goods:[],
				navs:[
					{
					icon:'iconfont icon-ziyuan',
					title:'热卖超市',
					path:'/pages/goods/goods'
				},
					{
					icon:'iconfont icon-guanyuwomen',
					title:'联系我们',
					path:'/pages/contact/contact'
				},
					{
					icon:'iconfont icon-tupian',
					title:'社区图片',
					path:'/pages/pics/pics'
				},
					{
					icon:'iconfont icon-shipin',
					title:'学习视频',
					path:'/pages/videos/videos'
				}


				],
			}
		},
		onLoad() {
			this.getSwiper()
			this.getHotGoods()
		},
		methods: {
		async	getSwiper(){
				const res = await this.$myRequest({
					url:'/api/getlunbo'
				})
				this.swipers=res.data.message
			},
			async getHotGoods(){
				const res= await this.$myRequest({
					url:'/api/getgoods?pageindex=1'
				})
			this.goods=res.data.message
			},
			navItemClick(url){
				uni.navigateTo({					
					url
				})
			},
			goGoodsDetail(id){
				uni.navigateTo({
					url:'/pages/goods-detail/goods-detail?id='+id
				})
			}
		}
	}
</script>

<style lang="scss">
		.home{
			swiper{
				width: 750rpx;
				height: 380rpx;
				image{
					height: 100%;
					width: 100%;
				}
			}
			.nav{
				display:flex;
				.nav-item{
					width: 25%;
					text-align: center;
					view{
						width: 120rpx;
						height: 120rpx;
						background: #b50e03;
						border-radius: 60rpx;
						margin:10px auto ;
						line-height: 120rpx;
						color: #fff;
						font-size: 50rpx;
					}
					.icon-tupian{
						font-size: 45rpx;
					}
					text{
						font-size: 30rpx;
					}
				}
			}
			.hot-goods{
				background: #eee;
				overflow: hidden;
				margin-top: 10px;
				.title{
					height: 50px;
					line-height: 50px;
					color: #b50e03;
					text-align: center;
					letter-spacing: 20px;
					background: #fff;
					margin: 7rpx 0;
				}
				
			}
		}
</style>
