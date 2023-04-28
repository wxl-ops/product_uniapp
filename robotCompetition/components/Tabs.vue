<!--
 * @Author: leslie
 * @Date: 2021-02-15 13:29:48
 * @LastEditors: leslie
 * @LastEditTime: 2021-05-05 16:27:06
 * @Description: Tabs组件
-->
<template>
	<div :id="id" class="page-tabs" :class="[`is-${type}`]">
		<scroll-view scroll-x class="tabs-scroll" :scroll-left="scrollLeft" scroll-with-animation>
			<view class="tabbar">
				<template v-for="(item, index) in list">
					<view :id="`tabbar-item-${index}`" :key="index" class="tabbar-item" @click="tapItem(index, item.key)">
						<view v-if="type === 'nav' && index > 0" class="tabbar-item__border"></view>
						<view class="tabbar-item-label" :class="{ active: currentIndex === index }">
							{{ item.name }}

							<template v-if="currentIndex === index">
								<view v-if="['article', 'simple'].includes(type)" class="tabbar-item-bottom"></view>
								<!-- <image v-if="['nav', 'nav-detail'].includes(type)" class="tabbar-active__icon" mode="aspectFit" src="/static/image/home/tab-active.svg" alt=""></image> -->
							</template>
						</view>
					</view>
				</template>
			</view>
		</scroll-view>
	</div>
</template>

<script>
export default {
	name: 'ComponentsTabs',
	model: {
		prop: 'value',
		event: 'input'
	},
	props: {
		// 当前活动tab的索引
		value: {
			type: Number,
			default: 0
		},
		// 需循环的标签列表
		list: {
			type: Array,
			default() {
				return [];
			}
		},
		// 未选中项的颜色
		inactiveColor: {
			type: String,
			default: 'rgba(0, 0, 0, 0.3)'
		},
		// 选中项的主题颜色
		activeColor: {
			type: String,
			default: '#182987'
		},
		// 字体大小
		fontSize: {
			type: [String, Number],
			default: 28
		},
		// 字体大小
		activeFontSize: {
			type: [String, Number],
			default: 32
		},
		// tab 可选的类型
		type: {
			type: String,
			default: 'article',
			validator(value) {
				return ['article', 'nav', 'nav-detail', 'simple'].includes(value);
			}
		}
	},
	data() {
		return {
			scrollLeft: 0, // 滚动scroll-view的左边滚动距离
			tabQueryInfo: [], // 存放对tab菜单查询后的节点信息
			componentWidth: 0, // 屏幕宽度，单位为px
			parentLeft: 0, // 父元素(tabs组件)到屏幕左边的距离
			currentIndex: 0
		};
	},
	computed: {
		// tab的样式
		tabItemStyle() {
			return index => {
				const style = {};
				if (index === this.currentIndex) {
					style.color = this.activeColor;
					style['font-size'] = this.activeFontSize + 'rpx';
				} else {
					style.color = this.inactiveColor;
					style['font-size'] = this.fontSize + 'rpx';
				}
				return style;
			};
		}
	},
	watch: {
		value: {
			immediate: true,
			deep: true,
			handler(nVal, oVal) {
				// 视图更新后再执行移动操作
				if (nVal !== oVal) {
					this.$nextTick(() => {
						let currentIndex = 0;
						this.list.map((item, index) => {
							if (item.key === nVal) {
								currentIndex = index;
							}
							return item;
						});
						this.currentIndex = currentIndex;
						this.scrollByIndex();
					});
				}
			}
		}
	},
	mounted() {
		this.init();
	},
	methods: {
		// 设置一个init方法，方便多处调用
		async init() {
			// 获取tabs组件的尺寸信息
			const tabRect = await this.$getRect('#' + this.id);
			// tabs组件距离屏幕左边的宽度
			this.parentLeft = tabRect.left;
			// tabs组件的宽度
			this.componentWidth = tabRect.width;
			this.getTabRect();
		},
		// 点击某一个tab菜单
		tapItem(index, key) {
			this.$emit('input', key);
			this.currentIndex = index;
			this.$nextTick(() => {
				this.scrollByIndex();
			});
		},
		// 查询tab的布局信息
		getTabRect() {
			// 创建节点查询
			const query = uni.createSelectorQuery().in(this);
			// 历遍所有tab，这里是执行了查询，最终使用exec()会一次性返回查询的数组结果
			for (let i = 0; i < this.list.length; i++) {
				// 只要size和rect两个参数
				query.select(`#tabbar-item-${i}`).fields({
					size: true,
					rect: true
				});
			}
			// 执行查询，一次性获取多个结果
			query.exec(
				function(res) {
					this.tabQueryInfo = res;
					// 初始化滚动条和移动bar的位置
					this.scrollByIndex();
				}.bind(this)
			);
		},
		// 滚动scroll-view，让活动的tab处于屏幕的中间位置
		scrollByIndex() {
			// 当前活动tab的布局信息，有tab菜单的width和left(为元素左边界到父元素左边界的距离)等信息
			const tabInfo = this.tabQueryInfo[this.currentIndex];
			if (!tabInfo) return;
			// 活动tab的宽度
			const tabWidth = tabInfo.width;
			// 活动item的左边到tabs组件左边的距离，用item的left减去tabs的left
			const offsetLeft = tabInfo.left - this.parentLeft;
			// 将活动的tabs-item移动到屏幕正中间，实际上是对scroll-view的移动
			const scrollLeft = offsetLeft - (this.componentWidth - tabWidth) / 2;
			this.scrollLeft = scrollLeft < 0 ? 0 : scrollLeft;
		}
	}
};
</script>

<style lang="scss" scoped>
.page-tabs {
	width: 100%;
	max-width: 100vw;
	background-color: #fff;
	box-shadow: 0 4rpx 12rpx rgba(0, 0, 0, 0.06);
	.tabbar {
		display: flex;

		/* padding: 36rpx 0; */

		.tabbar-item {
			position: relative;
			display: flex;
			flex-basis: 0;
			flex-grow: 1;
			align-items: center;
			justify-content: center;
			height: 100%;
			padding: 36rpx 0;
			font-size: 28rpx;
			line-height: 40rpx;
			color: #989898;

			.tabbar-item-label {
				position: relative;
				text-align: center;

				&.active {
					font-weight: 700;
					color: #1d74ff;
				}
			}

			&__border {
				position: absolute;
				top: 30rpx;
				left: 0;
				width: 1rpx;
				height: 40rpx;
				background-color: #d8d8d8;
				// transform: translate3d(0, -50%, 0);
			}

			.tabbar-item-bottom {
				position: absolute;
				bottom: -12rpx;
				left: 50%;
				width: 56rpx;
				height: 4rpx;
				background-color: #1d74ff;
				transform: translate3d(-50%, 0, 0);
			}

			.tabbar-active__icon {
				position: absolute;
				bottom: 0rpx;
				left: 50%;
				width: 68rpx;
				height: 8rpx;
				transform: translate3d(-50%, 0, 0);
			}
		}
	}

	&.is-nav {
		.tabbar {
			padding: 0;
		}
	}

	&.is-nav,
	&.is-nav-detail {
		box-shadow: none;

		.tabbar-item {
			padding: 28rpx 24rpx;
			font-size: 32rpx;
			font-weight: 400;
			line-height: 44rpx;
			color: rgba($color: #070707, $alpha: 0.44);

			// &.bordered {
			//   border-left: 1rpx solid rgba($color: #070707, $alpha: 0.2);
			// }

			.tabbar-item-label {
				&.active {
					color: #000;
				}
			}
		}
	}

	&.is-article .tabbar .tabbar-item {
		flex-basis: unset;
		// min-width: 25%;
		min-width: 33%;
		white-space: nowrap;
	}

	&.is-simple {
		.tabbar {
			display: block;
			text-align: center;

			.tabbar-item {
				display: inline-block;

				& + .tabbar-item {
					margin-left: 68rpx;
				}
			}
		}
	}
}
</style>
