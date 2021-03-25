<template>
	<view>
		<label>second</label>
		<u-tabbar :list="tarbar" :mid-button= "false"></u-tabbar>
	</view>
	
</template>

<script>
	export default {
		data() {
			return {
				tarbar: ''
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
			]
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
