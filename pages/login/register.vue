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
			Register</h1>
			
				<input 	v-model="phoneData"
					type="text"
					maxlength="11"
					placeholder="电话"
					clearable
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
					clearable
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
					
				<input 	v-model="verCode"
					type="number"
					maxlength="4"
					placeholder="验证码"
					clearable
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
				transition: 0.25s;">注册</button>	
												
			
				
				<view class="footer">
					<text @tap="isShowAgree" style="font-size: 25rpx; color: #808080;" > 同意</text>
					<text>|</text>
					<!-- 协议地址 -->
					<navigator url="" open-type="navigate" style="font-size: 25rpx; color: #808080;">《协议》</navigator>
					<text>|</text>
					<navigator url="login" open-type="navigate" style="font-size: 25rpx; color: #808080;">返回登陆</navigator>
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
				verCode:"", //验证码
			}
		},
		onLoad() {

		},		
		methods: {
			isShowAgree(){
					//是否选择协议
					_this.showAgree = !_this.showAgree;
				},
			getVerCode(){
				//获取验证码
				if (_this.phoneData.length != 11) {
					 uni.showToast({
						icon: 'none',
						position: 'bottom',
						title: '手机号不正确'
					});
					return false;
				}
				console.log("获取验证码")
				this.$refs.runCode.$emit('runCode'); //触发倒计时（一般用于请求成功验证码后调用）
				uni.showToast({
					icon: 'none',
					position: 'bottom',
					title: '模拟倒计时触发'
				});
				
				setTimeout(function(){
					_this.$refs.runCode.$emit('runCode',0); //假装模拟下需要 终止倒计时
					uni.showToast({
						icon: 'none',
						position: 'bottom',
						title: '模拟倒计时终止'
					});
				},3000)
			},
			startReg() {
				//注册
				if (this.showAgree == false) {
					uni.showToast({
						icon: 'none',
						position: 'bottom',
						title: '请先同意《协议》'
					});
					return false;
				}
				if (this.phoneData.length !=11) {
					uni.showToast({
						icon: 'none',
						position: 'bottom',
						title: '手机号不正确'
					});
					return false;
				}
				if (this.passData.length < 6) {
					uni.showToast({
						icon: 'none',
						position: 'bottom',
						title: '密码不正确'
					});
					return false;
				}
				if (this.verCode.length != 4) {
					uni.showToast({
						icon: 'none',
						position: 'bottom',
						title: '验证码不正确'
					});
					return false;
				}
				console.log("注册成功")
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
		font-size: 20rpx;
		margin-left: 15rpx;
		margin-right: 15rpx;
		color: #8f9294;
	}
</style>
