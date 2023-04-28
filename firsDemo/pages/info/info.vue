<template>
	<view>
		<view class="content">
			<view class="title">{{ title }}...</view>
			<view class="art-content"><rich-text class="richText" :nodes="strings"></rich-text></view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			title: '哈哈哈',
			strings: ''
		};
	},
	onInit({ newsid }) {
		console.log('此时运行到了onInit', this.title, newsid);
	},
	onLoad: function(e) {
		console.log(e);
		uni.request({
			url: 'https://unidemo.dcloud.net.cn/api/news/36kr/' + e.newsid,
			method: 'GET',
			data: {},
			success: res => {
				console.log(res);
				this.title = res.data.title;
				this.strings = res.data.content;
			},
			fail: () => {},
			complete: () => {}
		});
	},
	onReady(a, b, c) {
		console.log('这是onReady方法', a, b, c);
	},
	onHide() {
		console.log('这是onHide方法', a, b, c);
	},
	onUnload(a, b, c) {
		console.log('这是onUnload方法', a, b, c);
	}
};
</script>

<style>
.content {
	padding: 10upx 2%;
	width: 96%;
	flex-wrap: wrap;
}

.title {
	line-height: 2em;
	font-weight: 700;
	font-size: 38upx;
}

.art-content {
	line-height: 2em;
}
</style>
