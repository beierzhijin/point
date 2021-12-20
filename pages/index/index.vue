<style lang="scss" scoped>
	.swiper {
		height: calc(100vh - 40px);
	}

	image {
		will-change: transform;
	}
</style>

<template>
	<view>
		<u-tabs-swiper ref="uTabs" :list="tabList" :is-scroll="false" :current="current" @change="change"
			swiperWidth="750">
		</u-tabs-swiper>
		<swiper class="swiper" :current="swiperCurrent" @transition="transition" @animationfinish="animationfinish">
			<swiper-item class="swiper-item" v-for="(item, index) in tabList" :key="index">
				<view class="w-full h-full" style="padding-top: 20px;">
					<view v-show="current === 0">
						<view class="u-flex u-row-between">
							<view class="u-flex-4">
								<view class="u-flex" style="padding-left: 20px;margin-bottom: 8px;">
									<text>A：</text>
									<u-input v-model="up_0_A" :type="number" border-color="#3779fd" :clearable="false"
										border />
								</view>
								<view class="u-flex" style="padding-left: 20px;">
									<text>B：</text>
									<u-input v-model="up_0_B" :type="number" border-color="#3779fd" :clearable="false"
										border />
								</view>
							</view>
							<view class="u-flex-2" style="padding-right: 10px;">
								<u-button @click="calc0" type="primary" ripple>检查计算结果</u-button>
							</view>
						</view>
						<view class="" style="padding: 20px 0;text-align: center;">
							<text style="color: #007AFF;">⬇️⬇️⬇️ 计算结果：{{result}} ⬇️⬇️⬇️️️</text>
						</view>
						<view class="u-flex" style="padding-left: 20px;margin-bottom: 8px;">
							<text>C - 目标价一：</text>
							<u-input v-model="up_0_C_1" :type="number" border-color="#3779fd" :clearable="false"
								border />
						</view>
						<view class="u-flex" style="padding-left: 20px;">
							<text>C - 目标价二：</text>
							<u-input v-model="up_0_C_2" :type="number" border-color="#3779fd" :clearable="false"
								border />
						</view>
						<view class="u-flex u-row-center" style="margin-top: 20px;">
							<image src="../../static/0.png" mode="widthFix"></image>
						</view>
					</view>
					<view v-show="current === 1">
						<view class="u-flex u-row-between">
							<view class="u-flex-4">
								<view class="u-flex" style="padding-left: 20px;margin-bottom: 8px;">
									<text>A：</text>
									<u-input v-model="up_1_A" :type="number" border-color="#3779fd" :clearable="false"
										border />
								</view>
								<view class="u-flex" style="padding-left: 20px;">
									<text>B：</text>
									<u-input v-model="up_1_B" :type="number" border-color="#3779fd" :clearable="false"
										border />
								</view>
							</view>
							<view class="u-flex-2" style="padding-right: 10px;">
								<u-button @click="calc1" type="primary" ripple>检查计算结果</u-button>
							</view>
						</view>
						<view class="" style="padding: 20px 0;text-align: center;">
							<text style="color: #007AFF;">⬇️⬇️⬇️ 计算结果：{{result1}} ⬇️⬇️⬇️️️</text>
						</view>
						<view class="u-flex" style="padding-left: 20px;margin-bottom: 8px;">
							<text>C - 目标价一：</text>
							<u-input v-model="up_1_C_1" :type="number" border-color="#3779fd" :clearable="false"
								border />
						</view>
						<view class="u-flex" style="padding-left: 20px;">
							<text>C - 目标价二：</text>
							<u-input v-model="up_1_C_2" :type="number" border-color="#3779fd" :clearable="false"
								border />
						</view>
						<view class="u-flex u-row-center" style="margin-top: 20px;">
							<image src="../../static/1.png" mode="widthFix"></image>
						</view>
					</view>
				</view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				tabList: [{
						name: '下跌测反弹'
					},
					{
						name: '上涨测回调'
					}
				],
				number: 'digit',
				up_0_A: null,
				up_0_B: null,
				up_1_A: null,
				up_1_B: null,
				current: 0,
				result: '',
				result1: ''
			}
		},
		computed: {
			up_0_C_1() {
				let temp = Number(this.up_0_B) + Number((this.up_0_A - this.up_0_B) * 0.4936)
				return temp.toFixed(4)
			},
			up_0_C_2() {
				let temp = Number(this.up_0_B) + Number((this.up_0_A - this.up_0_B) * 0.73886)
				return temp.toFixed(4)
			},
			up_1_C_1() {
				let temp = Number(this.up_1_B) - Number((this.up_1_B - this.up_1_A) * 0.5037)
				return temp.toFixed(4)
			},
			up_1_C_2() {
				let temp = Number(this.up_1_B) - Number((this.up_1_B - this.up_1_A) * 0.74915)
				return temp.toFixed(4)
			},
		},
		methods: {
			calc0() {
				let result = (Number(this.up_0_B) + Number((this.up_0_A - this.up_0_B) * 0.4936)).toFixed(4)
				let result1 = (Number(this.up_0_B) + Number((this.up_0_A - this.up_0_B) * 0.73886)).toFixed(4)
				if (result === this.up_0_C_1 && result1 === this.up_0_C_2) {
					this.result = '正确'
				} else {
					this.result = '错误'
				}
			},
			calc1() {
				let result = (Number(this.up_1_B) - Number((this.up_1_B - this.up_1_A) * 0.5037)).toFixed(4)
				let result1 = (Number(this.up_1_B) - Number((this.up_1_B - this.up_1_A) * 0.74915)).toFixed(4)
				if (result === this.up_1_C_1 && result1 === this.up_1_C_2) {
					this.result1 = '正确'
				} else {
					this.result1 = '错误'
				}
			},
			change(index) {
				this.swiperCurrent = index
			},
			// swiper-item左右移动，通知tabs的滑块跟随移动
			transition(e) {
				let dx = e.detail.dx;
				this.$refs.uTabs.setDx(dx);
			},
			// 由于swiper的内部机制问题，快速切换swiper不会触发dx的连续变化，需要在结束时重置状态
			// swiper滑动结束，分别设置tabs和swiper的状态
			animationfinish(e) {
				let current = e.detail.current;
				this.$refs.uTabs.setFinishCurrent(current);
				this.swiperCurrent = current;
				this.current = current;
			},
		}
	}
</script>
