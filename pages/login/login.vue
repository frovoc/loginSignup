<template>
	<view class="content">
		
		<view class="box" style="width: 300px;
            padding: 40px;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: #191919;
            text-align: center;">
			
			<h1 style="color: white;
			text-transform: uppercase;
			font-weight: 500;">
			LogIn</h1>
			
			<input 	v-model="phoneData"
				type="text"
				maxlength="11"
				placeholder="用户名/电话"
				style=" border: 0;
				background: none;
				display: block;
				margin: 20px auto;
				text-align: center;
				border: 2px solid #3498db;
				padding: 14px 10px;
				width: 200px;
				outline: none;
				color: white;
				border-radius: 24px;
				transition: 0.25s;">
				
			<input 	v-model="passData"
				type="password"
				maxlength="11"
				placeholder="密码"
				style=" border: 0;
				background: none;
				display: block;
				margin: 20px auto;
				text-align: center;
				border: 2px solid #3498db;
				padding: 14px 10px;
				width: 200px;
				outline: none;
				color: white;
				border-radius: 24px;
				transition: 0.25s;">
				
			<button type="button"
			@click="startLogin"
			style="border: 0;
			background: none;
			display: block;
			margin: 20px 180rpx;
			text-align: center;
			border: 2px solid #2ecc71;
			padding: 2px 2px;
			outline: none;
			color: white;
			border-radius: 24px;
			transition: 0.25s;">登录</button>	
			
			<view class="footer">
				<navigator url="forget" open-type="navigate" class="text" style="font-size: 25rpx; color: #808080;">找回密码</navigator>
				<text>|</text>
				<navigator url="register" open-type="navigate" class="text" style="font-size: 25rpx; color: #808080;">注册账号</navigator>	
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				phoneData:'', //用户/电话
				passData:'', //密码
			}
		},
		onLoad() {

		},		
		methods: {
			isLogin(){
				//判断缓存中是否登录过，直接登录
				// try {
				// 	const value = uni.getStorageSync('setUserData');
				// 	if (value) {
				// 		//有登录信息
				// 		console.log("已登录用户：",value);
				// 		_this.$store.dispatch("setUserData",value); //存入状态
				// 		uni.reLaunch({
				// 			url: '../../../pages/index',
				// 		});
				// 	}
				// } catch (e) {
				// 	// error
				// }
			},
			startLogin(e){
				console.log(e)
				//登录
				if (this.phoneData.length == "") {
					 uni.showToast({
						icon: 'none',
						position: 'bottom',
						title: '用户名不能为空'
					});
					return;
				}
				if (this.passData.length < 5) {
					uni.showToast({
						icon: 'none',
						position: 'bottom',
						title: '密码不正确'
					});
					return;
				}
				
				console.log("登录成功")
				
				// uni.showLoading({
				// 	title: '登录中'
				// });
				// getLogin()
				// .then(res => {
				// 	//console.log(res)
				// 	//简单验证下登录（不安全）
				// 	if(_this.phoneData==res.data.username && _this.passData==res.data.password){
				// 		let userdata={
				// 			"username":res.data.username,
				// 			"nickname":res.data.nickname,
				// 			"accesstoken":res.data.accesstoken,
				// 		} //保存用户信息和accesstoken
				// 		_this.$store.dispatch("setUserData",userdata); //存入状态
				// 		try {
				// 			uni.setStorageSync('setUserData', userdata); //存入缓存
				// 		} catch (e) {
				// 			// error
				// 		}
				// 		uni.showToast({
				// 			icon: 'success',
				// 			position: 'bottom',
				// 			title: '登录成功'
				// 		});
				// 		uni.reLaunch({
				// 			url: '../../../pages/index',
				// 		});
				// 	}else{
				// 		_this.passData=""
				// 		uni.showToast({
				// 			icon: 'error',
				// 			position: 'bottom',
				// 			title: '账号或密码错误，账号admin密码admin'
				// 		});
				// 	}
				// 	uni.hideLoading();
				// }).catch(err => {
				// 	uni.hideLoading();
				// })
			}

		}
	}
</script>

<style>
	page{
		margin: 0;
		padding: 0;
		font-family: sans-serif;
		background: #34495e;
	}
	.footer{
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		font-size: 28rpx;
		margin-top: 64rpx;
		color: rgba(0,0,0,0.7);
		text-align: center;
		height: 40rpx;
		line-height: 40rpx;
	}
	.footer text{
		font-size: 40rpx;
		margin-left: 15rpx;
		margin-right: 15rpx;
		color: #8f9294;
	}
</style>
