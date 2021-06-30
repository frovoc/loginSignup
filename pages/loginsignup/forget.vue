<template>
	<view class="forget">
		
		<view class="content">
			<!-- head -->
			<view class="header">
				<el-image :src="src"></el-image>			
			</view>
			<!-- 主体 -->
			<view class="main">
				<view class="tips">若你忘记了密码，可在此重置新密码。</view>
				<el-input
					v-model="phoneData"
					type="text"
					maxlength="11"
					placeholder="请输入手机号码"
					clearable>
				</el-input>
				<el-input
					v-model="passData"
					type="password"
					maxlength="11"
					placeholder="请输入新密码"
					show-password
					clearable>
				</el-input>
				<el-input
					v-model="verCode"
					type="number"
					maxlength="4"
					placeholder="验证码"
					clearable>
				</el-input>
				
				<!-- <el-button				
				isShowCode
				codeText="获取重置码"
				class="wbutton"
				setTime="30"
				ref="runCode"
				@click.native="getVerCode()">
				获取验证码</el-button> -->
				<el-button 
				class="wbutton"
				@click.native="startRePass()">
				重置密码</el-button>
				<navigator url="login" open-type="navigate">返回登陆</navigator>
				
			</view>
		</view>		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				src: 'https://cube.elemecdn.com/6/94/4d3ea53c084bad6931a56d5158a48jpeg.jpeg',
				phoneData: "", //电话
				passData: "", //密码
				verCode:"", //验证码
			}
		},
		
		methods: {
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
			startRePass() {
				//重置密码

				if (this.phoneData.length != 11) {
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
				console.log("重置密码成功")
			}			
		}
	}
</script>

<style>
	@import url("main.css");
</style>
