<template>
	<view class="container">
		<view class="uni-list">
			<view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item, index) in news" :key="index" @tap="openinfo(item.post_id)">
				<view class="uni-media-list">
					<image class="uni-media-list-logo" :src="item.author_avatar"></image>
					<view class="uni-media-list-body">
						<view class="uni-media-list-text-top ellipsis">{{ item.title }}</view>
						<view class="uni-media-list-text-bottom">{{ item.created_at }}</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			news: []
		};
	},
	methods: {
		openinfo(id) {
			console.log('出发时间', id);
			uni.navigateTo({
				url: `/pages/info/info?newsid=${id}`
			});
		}
	},
	onShow(a, b, c) {
		console.log('这是onShow方法', a, b, c);
	},
	onLoad() {
		uni.request({
			url: 'https://unidemo.dcloud.net.cn/api/news',
			method: 'GET',
			success: res => {
				this.news = res.data;
			}
		});
	}
};
</script>

<style lang="less">
.ellipsis {
	overflow: hidden;
	text-overflow: ellipsis;
	display: -webkit-box;
	-webkit-line-clamp: 2;
	-webkit-box-orient: vertical;
}
.container {
	padding: 20px;
	font-size: 14px;
	line-height: 24px;
	.uni-list {
		display: flex;
		flex-wrap: wrap;
		.uni-list-cell {
			border-bottom: 1px solid #eee;
			.uni-media-list {
				display: flex;

				.uni-media-list-logo {
					width: 80px;
					height: 80px;
					flex: none;
				}
				.uni-media-list-body {
					height: auto;
					display: flex;
					flex-direction: column;
					justify-content: space-between;
					padding: 5px 0;
				}
				.uni-media-list-text-top {
					line-height: 1.6em;
				}
				.uni-media-list-text-bottom {
					display: block;
				}
			}
		}
	}
}
</style>
