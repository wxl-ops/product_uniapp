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
		<!-- <RobotTabs :list="tabs" /> -->
		<!-- <view class="tj-robot__tabbar">
      <template v-for="(item,index) in tabs">
        <view :key="item.id" class="tj-robot__tabbar-item">
          <view class="tj-robot__tabbar-item-label" :class="tabsCurrent == index ? 'active' : ''" @click="handleCurrentPage(index)">
            {{ item.name }}
            <view v-show="tabsCurrent == index" class="tj-robot__tabbar-item-bottom"></view>
          </view>
        </view>
      </template>
    </view> -->
		<view class="tj-robot__body">
			<view class="tj-robot-cont">
				<view class="tj-robot-cont-hd">
					<view class="tj-robot__header"><view class="tj-robot-menu__title">赛程安排</view></view>
				</view>
				<view class="tj-robot-cont-bd">
					<view class="tj-robot__markdown">
						<view class="tj-robot-text-level-two">
							2021RoboCup机器人世界杯中国赛暨亚太机器人世界杯天津国际邀请赛（简称“RCAP天津国际邀请赛”）作为天津市第五届世界智能大会的重要组成部分，于2021年5月19日-22日在天津空港体育中心举办。2021
							RCAP亚太机器人世界杯天津国际邀请赛首次联手RoboCup机器人世界杯中国赛，将在津门为全国观众呈现一场盛大的国际机器人竞技盛宴。同时，本次大赛采用的“线上线下+国内国外”同步开展的联动赛事模式，也将为本届赛事增加新的亮点。

							<image src="./img/dUhDawZyS1yMwUDuSgrMqw.png" class="tj-robot-text-level-two-img"></image>
						</view>
						<view class="tj-robot-case-title__content">
							<view class="case-title-title">RoboCup机器人世界杯赛</view>
							<view class="cases-title-title__border"></view>
						</view>
						<view class="tj-robot-text-level-two">
							<view class="tj-robot-text-level-two-p">
								机器人世界杯赛，是当前国际上级别最高、规模最大、影响最广泛的机器人赛事，由RoboCup国际联合会主办。RoboCup主要目的是通过提供一个标准的易于评价的比赛平台，促进MAS(Multi-Agent
								System）和DAI(Distributed Artificial
								Intelligence）的研究与发展，其最终目标是经过五十年左右的研究，使机器人足球队能战胜人类足球冠军队。机器人世界杯赛融合丰富的学术研讨会议，工业与机器人展览会和世界顶级的机器人竞赛为一体，在过去20年中，引领了人工智能、机器人科学与机器人教育的发展。-22日在天津空港体育中心举办。2021
								本次大赛共设有四大赛项包含12个分赛项，分别为RoboCup足球机器人比赛（类人组、中型组、仿真2D组、仿真3D组、小型组、标准平台组），RoboCup救援组比赛（救援机器人组、救援仿真组），RoboCup家庭组（开放平台组、标准平台组）比赛以及RCAP+国内国外”同步开展的联动赛事模式，也将为本届赛事增加新的亮点。
							</view>
							<view class="tj-robot-text-level-two-p">
								自1997年首届机器人比赛在日本名古屋成功举办以来，分别在法国、瑞典、澳大利亚、美国、德国、韩国、意大利、葡萄牙、中国、奥地利、新加坡、荷兰、巴西、加拿大等十余个国家和地区进行了比赛。中国分别于2008年在江苏苏州举办了第12届和2015年在安徽合肥举办了第19届机器人世界杯赛。目前已有来自全球50多个国家的队员参加机器人世界杯，参赛者包括世界众多知名学府和科研机构与教育机构。-22日在天津空港体育中心举办。2021
								本次大赛共设有四大赛项包含12个分赛项，分别为RoboCup足球机器人比赛（类人组、中型组、仿真2D组、仿真3D组、小型组、标准平台组），RoboCup救援组比赛（救援机器人组、救援仿真组），RoboCup家庭组（开放平台组、标准平台组）比赛以及RCAP+国内国外”同步开展的联动赛事模式，也将为本届赛事增加新的亮点。
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	name: 'IndexPartner',
	data() {
		return {
			pageLoad: false
		};
	},
	onLoad() {
		setTimeout(() => {
			this.pageLoad = true;
		}, 30);
	}
};
</script>

<style lang="scss" scoped>
@import './intro.scss';
</style>
