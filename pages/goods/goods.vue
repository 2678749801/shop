<template>
	<view class="goods-list">
		<good-list :goods="goods"></good-list>
		<view class="isOver" v-if="flag">--------我是有底线的---------</view>
	</view>
</template>

<script>
	import goodList from '../../components/goods-list/goods-list.vue'
	export default {
		data() {
			return {
				pageindex:1,
				goods:[],
				flag:false,
			}
		},
		onLoad() {
			this.getGoodList()
		},
		components:{
			goodList
		},
		methods: {
			async getGoodList(){
				const res=await this.$myRequest({
					url:'/api/getgoods?pageindex='+this.pageindex
					})
					this.goods=[...this.goods,...res.data.message]
			}
		},
		onReachBottom(){
			if(this.goods.length<this.pageindex*10) return this.flag=true
			this.pageindex++
			this.getGoodList()
		},
		onPullDownRefresh() {
			this.pageindex=1,
			this.goods=[],
			this.flag=false,
			setTimeout(()=>{
				this.getGoodList()
				uni.stopPullDownRefresh()
			},1000)
			
		}
	}
</script>

<style lang="scss">
.goods-list{
		background-color: #eee;
}
.isOver{
	width: 100%;
	height: 50px;
	line-height: 50px;
	text-align: center;
	background: #fff;
	font-size: 28rpx;
}
</style>
