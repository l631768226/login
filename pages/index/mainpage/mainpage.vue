<template>
	<view>
		<view class="u-page">
			
		</view>
		
		<u-tabbar v-model="current" :list="list" :mid-button="false"></u-tabbar>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list:[{
					iconPath: "home",
					selectedIconPath: "home-fill",
					text:"首页",
					customIcon: false,
				},
				{
					iconPath: 'photo',
					selectedIconPath: 'photo-fill',
					text: '照片',
					customIcon: false
				},
				{
					iconPath: 'play-right',
					selectedIconPath: 'play-right-fill',
					text: '视频',
					customIcon: false,
				},
				{
					iconPath: 'account',
					selectedIconPath: 'account-fill',
					text: '我的',
					customIcon: false,
					isDot: false
				}],
				current: 0
			}
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
