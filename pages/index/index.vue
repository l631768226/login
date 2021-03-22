<template>
	<view class="content">
		<view>
			<u-field
				v-model="uname"
				label="用户名"
				placeholder="请输入用户名">
			</u-field>
			
			<u-field
				v-model="pwd"
				label="密码"
				placeholder="请输入密码">
			</u-field>
			
			<u-button @click="login_click">登录</u-button>
		</view>
		
		<view>
			<u-toast ref="uToast"></u-toast>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				uname:'',
				pwd:''
			}
		},
		onLoad() {
			
		},
		methods: {
			showToast(str){
				this.$refs.uToast.show({
					title: str,
					type: 'error'
				})
			},
			login_click:function(e){
				uni.request({
					url:'http://192.168.4.232:8999/user/login',
					method:'POST',
					dataType:'json',
					data:{
						'data':{
							'username':this.uname,
							'password':this.pwd
						}
					},
					header:{
						'Content-Type': 'application/json;charset=utf-8'
					},
					success: (res) => {
						console.log(res.data)
						console.log(typeof res.data)
						var resDataStr = JSON.stringify(res.data)
						var resData = JSON.parse(resDataStr)
						var code = resData.code
						console.log(code)
						if(code > 0){
							uni.navigateTo({
								url:'/pages/index/mainpage/mainpage'
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
			},
			input_uname(e){
				this.uname = e.detail.value;
			},
			input_pwd(e){
				this.pwd = e.detail.value;
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
