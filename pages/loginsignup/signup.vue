<template>
	<view class="signup">
		<view class="content">
			<!-- head -->
			<view class="header">
				<el-image :src="src"></el-image>			
			</view>
			<!-- 主体 -->
			<view class="main">
				<el-input
					placeholder="电话"
					v-model="phoneData"
					type="text"
					maxlength="11"
					:focus="isFocus"
					clearable>
				</el-input>
				<el-input 
					placeholder="请输入密码" 
					v-model="passData"
					type="password"
					maxlength="11"
					show-password
					clearable>
				</el-input>
				<el-input
					v-model="verCode"
					type="number"
					maxlength="4"
					placeholder="验证码"
					clearable
					ref="runCode"
					@setCode="getVerCode()">
				</el-input>
				
				<el-button 
				type="primary"
				@click.native="startReg()"					 
				>注册</el-button>
				<navigator url="login" open-type="navigate">返回登陆</navigator>
				
				<!-- 底部信息 -->
				<view class="footer">
					<text 
						@tap="isShowAgree" 
					> 同意</text>
					<!-- 协议地址 -->
					<navigator url="" open-type="navigate">《协议》</navigator>
				</view>
			</view>
		</view>		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				src: 'https://cube.elemecdn.com/6/94/4d3ea53c084bad6931a56d5158a48jpeg.jpeg',
				input: '',
				phoneData:'', //用户/电话
				passData:'', //密码
				verCode:"", //验证码
				isFocus: true // 是否聚焦
			}
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
	@import url("main.css");
</style>
