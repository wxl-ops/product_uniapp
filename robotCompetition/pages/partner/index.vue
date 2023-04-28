<!--
 * @Author: leslie
 * @Date: 2021-03-25 18:33:34
 * @LastEditors: leslie
 * @LastEditTime: 2021-04-21 17:24:47
 * @Description: 合作伙伴-列表
-->
<template>
	<view v-if="pageLoad" class="tj-robot">
		<!-- <Tabs v-model="tabsCurrent" type="article" :list="tabs" /> -->
		<web-view :src="url" class="pageStyle"></web-view>
	</view>
</template>

<script>
// import Tabs from '@/components/Tabs';
export default {
	name: 'IndexPartner',
	// components: { Tabs },
	data() {
		return {
			url: 'pages/partner/intro',
			pageLoad: false,
			tabs: [{ id: 0, name: '关于大赛', key: 0 }, { id: 1, name: '组织机构', key: 1 }, { id: 2, name: '赛事介绍', key: 2 }, { id: 3, name: '日程安排', key: 3 }],
			pagePathName: ['intro', 'organization', 'competitionsIntro', 'competitionsPlan'],
			partnerList: ['关于大赛', '组织机构', '赛事介绍', '日程安排'],
			tabsCurrent: 0
		};
	},
	watch: {
		tabsCurrent(value = 0) {
			this.url = `/pages/partner/${this.pagePathName[value]}`;
		}
	},
	onLoad() {
		// uni.setNavigationBarTitle({
		// 	title: '机器人大赛'
		// });
		setTimeout(() => {
			this.pageLoad = true;
		}, 30);
	}
};
</script>

<style lang="scss" scoped>
.pageStyle {
	margin-top: 130rpx;
}
</style>
