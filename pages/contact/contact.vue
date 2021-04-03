<template>
	<view class="contact">
		<image src="http://www.itcast.cn/2018czydz/images/gywmban.jpg" class="img"></image>
		<view class="info">
			<view @click="phone">联系电话 13945412442(点击拨打)</view>
			<view>联系地址：哈尔滨商业大学</view>
		</view>
		<map class="map" :longitude="longitude" scale="14" :latitude="latitude"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude:126.57088,
				latitude:45.826205,
			}
		},
		methods: {
			phone(){
				uni.makePhoneCall({
					phoneNumber:'13945412442'
				})
			}
		}
	}
</script>

<style lang="scss">
.contact{
	.img{
		height: 320rpx;
	}
	.info{
		padding: 10rx 20rpx;
		font-size: 30rpx;
		view{
			line-height: 80rpx;
			border-bottom: 1px solid #eee;
		}
	}
	.map{
		width: 750rpx;
		height: 750rpx;
	}
}
</style>
