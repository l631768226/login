<template>
	<view>
		<view class="wrap">
<!-- 			<view class="u-tabs-box">
				<u-tabs-swiper active-color="#f29100" ref="tabs" :list="list" :current="current" 
				@change="change" :is-scroll="false"></u-tabs-swiper>
			</view> -->
<!-- 			<swiper class="swiper-box" :current="swipperCurrent" @transition="transitition" @animationfinish="animationfinish">
				<swiper-item class="swiper-item"> -->
					<scroll-view scroll-y style="height: 100%;width: 100%;" @scrolltolower="reachBottom">
						<view class="page-box">
							<view class="movie" v-for="(res, index) in movieList" :key="res.id" @click="click(res.id)">
								<view class = "top">
									<view class = 'movieName'>{{res.title}}</view>
									<view class="rank">{{res.rank}}</view>
								</view>
								<view class="item">
									<view class="left">
										<image :src="res.img"></image>
									</view>
								</view>
								<view class="bottom">
									<view>{{res.inq}}</view>
								</view>
							</view>
						</view>
					</scroll-view>
<!-- 				</swiper-item>
			</swiper> -->
				
		</view>
		<u-tabbar :list="tarbar" :mid-button= "false"></u-tabbar>
	</view>
	
</template>

<script>
	export default {
		data() {
			return {
				current: 0,
				swipperCurrent: 0,
				tarbar: '',
				list: [
					{
						name: "电影"
					},
					{
						name: "歌曲"
					}
				],
				movieList:[]
			}
		},
		onLoad() {
			this.tarbar = [{
				iconPath: "home",
				selectedIconPath: "home-fill",
				text:"首页",
				customIcon: false,
				pagePath: "/pages/index/mainpage/mainpage"
			},
			{
				iconPath: 'photo',
				selectedIconPath: 'photo-fill',
				text: '照片',
				customIcon: false,
				pagePath: "/pages/index/mainpage/second"
			},
			// {
			// 	iconPath: 'play-right',
			// 	selectedIconPath: 'play-right-fill',
			// 	text: '视频',
			// 	customIcon: false,
			// },
			// {
			// 	iconPath: 'account',
			// 	selectedIconPath: 'account-fill',
			// 	text: '我的',
			// 	customIcon: false,
			// 	isDot: false
			// }
			],
			
			uni.request({
				url:'http://192.168.4.232:8999/movie/allList',
				method:'POST',
				dataType:'json',
				data:{
					'data':{

					}
				},
				header:{
					'Content-Type': 'application/json;charset=utf-8'
				},
				success: (res) => {
					console.log(res)
					var resDataStr = JSON.stringify(res.data)
					var resData = JSON.parse(resDataStr)
					var code = resData.code
					if(code > 0){
						this.movieList = resData.data
						console.log("OK")
					}else{
						this.showToast(resData.msg)
					}
				
				},
				fail: (e) => {
					console.log(e)
					uni.showToast({
						title:'网络错误',
						duration:2000
					})
				}
			})
		},
		methods: {
			change(index){
				this.swipperCurrent = index;
			},
			click(id){
				console.log(id)
				uni.request({
					url:'http://192.168.4.232:8999/movie/detail',
					method:'POST',
					dataType:'json',
					data:{
						'data':{
							'id':id,
						}
					},
					header:{
						'Content-Type': 'application/json;charset=utf-8'
					},
					success: (res) => {
						console.log(res)

						var code = res.data.code
						console.log(code)
						if(code > 0){
							console.log(res.data.data.title)
							
							uni.navigateTo({
								url:'/pages/index/movieDetail?item=' + encodeURIComponent(JSON.stringify(res.data.data))
							})
							
						}else{
							this.showToast(resData.msg)
						}
					
					},
					fail: (e) => {
						console.log(e)
						uni.showToast({
							title:'网络错误',
							duration:2000
						})
					}
				})
			}
		}
	}
</script>

<style>

</style>

<style lang="scss" scoped>
	.movie{
		.top{
			display: flex;
		}
	}
	
</style>
