<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<navigator url="/pages/partner/intro">前往大赛简介页面</navigator>
			<navigator url="/pages/partner/organization">前往组织机构页面</navigator>
			<navigator url="/pages/partner/competitionsIntro">前往赛事介绍页面</navigator>
			<navigator url="/pages/partner/competitionsPlan">前往赛事安排页面</navigator>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			title: 'Hello'
		};
	},
	onLoad() {},
	methods: {}
};
</script>

<style>
.content {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}

.logo {
	height: 200rpx;
	width: 200rpx;
	margin-top: 200rpx;
	margin-left: auto;
	margin-right: auto;
	margin-bottom: 50rpx;
}

.text-area {
	display: flex;
	flex-direction: column;
	justify-content: center;
}

.title {
	font-size: 36rpx;
	color: #8f8f94;
}
</style>
