<template>
	<view class="uni-calendar-item__weeks-box" :class="{
		'uni-calendar-item--disable':weeks.disable,
		'uni-calendar-item--isDay':calendar.fullDate === weeks.fullDate && weeks.isDay,
		'uni-calendar-item--checked':(calendar.fullDate === weeks.fullDate && !weeks.isDay) ,
		'uni-calendar-item--multiple': weeks.multiple
		}"
	 @click="choiceDate(weeks)">
		<view class="uni-calendar-item__weeks-box-item">
			<text v-if="selected&&weeks.extraInfo" class="uni-calendar-item__weeks-box-circle"></text>
			<text class="uni-calendar-item__weeks-box-text" :class="{
				'uni-calendar-item--isDay-text': weeks.isDay,
				'uni-calendar-item--isDay':calendar.fullDate === weeks.fullDate && weeks.isDay,
				'uni-calendar-item--checked':calendar.fullDate === weeks.fullDate && !weeks.isDay,
				'uni-calendar-item--multiple': weeks.multiple,
				'uni-calendar-item--disable':weeks.disable,
				}">{{weeks.date}}</text>
			<text v-if="!lunar&&!weeks.extraInfo && weeks.isDay" class="uni-calendar-item__weeks-lunar-text" :class="{
				'uni-calendar-item--isDay-text':weeks.isDay,
				'uni-calendar-item--isDay':calendar.fullDate === weeks.fullDate && weeks.isDay,
				'uni-calendar-item--checked':calendar.fullDate === weeks.fullDate && !weeks.isDay,
				'uni-calendar-item--multiple': weeks.multiple,
				}"></text>
			<text v-if="lunar&&!weeks.extraInfo" class="uni-calendar-item__weeks-lunar-text" :class="{
				'uni-calendar-item--isDay-text':weeks.isDay,
				'uni-calendar-item--isDay':calendar.fullDate === weeks.fullDate && weeks.isDay,
				'uni-calendar-item--checked':calendar.fullDate === weeks.fullDate && !weeks.isDay,
				'uni-calendar-item--multiple': weeks.multiple,
				'uni-calendar-item--disable':weeks.disable,
				}">{{weeks.isDay?'今天': (weeks.lunar.IDayCn === '初一'?weeks.lunar.IMonthCn:weeks.lunar.IDayCn)}}</text>
			<text v-if="weeks.extraInfo&&weeks.extraInfo.info" class="uni-calendar-item__weeks-lunar-text" :class="{
				'uni-calendar-item--extra':weeks.extraInfo.info,
				'uni-calendar-item--isDay-text':weeks.isDay,
				'uni-calendar-item--isDay':calendar.fullDate === weeks.fullDate && weeks.isDay,
				'uni-calendar-item--checked':calendar.fullDate === weeks.fullDate && !weeks.isDay,
				'uni-calendar-item--multiple': weeks.multiple,
				'uni-calendar-item--disable':weeks.disable,
				}">{{weeks.extraInfo.info}}</text>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			weeks: {
				type: Object,
				default () {
					return {}
				}
			},
			calendar: {
				type: Object,
				default: () => {
					return {}
				}
			},
			selected: {
				type: Array,
				default: () => {
					return []
				}
			},
			lunar: {
				type: Boolean,
				default: false
			}
		},
		methods: {
			choiceDate(weeks) {
				this.$emit('change', weeks)
			}
		}
	}
</script>

<style lang="scss" scoped>
	.uni-calendar-item__weeks-box {
		flex: 1;
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		justify-content: center;
		align-items: center;
		color: #fff;
	}

	.uni-calendar-item__weeks-box-text {
		font-size: 30rpx;
		color: #333;
		background: transparent !important;
	}

	.uni-calendar-item__weeks-lunar-text {
		font-size: $uni-font-size-sm;
		color: $uni-text-color;
	}

	.uni-calendar-item__weeks-box-item {
		position: relative;
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		justify-content: center;
		align-items: center;
		width: 60rpx;
		height: 60rpx;
	}

	.uni-calendar-item__weeks-box-circle {
		// position: absolute;
		// top: -2px;
		// right: -5px;
		// width: 8px;
		// height: 8px;
		// border-radius: 10px;
		// background-color: $uni-color-error;
		// display: none;
		position: absolute;
		width: 18px;
		height: 18px;
		border: 3px solid #ffc693;
		border-radius: 18px;
		//background-color: #0FF;
		opacity: 0.5;
		top:3px

	}

	.uni-calendar-item--disable {
		// background-color: rgba(249, 249, 249, $uni-opacity-disabled);
		color: #b2bddd;
	}

	.uni-calendar-item--isDay-text {
		color: #333;
		background: transparent !important;
	}

	.uni-calendar-item--isDay {
		background-color: #f98116;
		opacity: 0.8;
		color: #fff;
		width: 30px;
		border-radius: 100px;
		text-align: center;
		margin: 0 auto;
	}

	.uni-calendar-item--extra {
		display: none;
		// color: $uni-color-error;
		// opacity: 0.8;
		// background: transparent !important;
	}

	.uni-calendar-item--checked {
		background-color: #f98116;
		color: #fff;
		opacity: 0.8;
		width: 30px !important;
		border-radius: 100px !important;
		text-align: center;
		margin: 0 auto;
	}

	.uni-calendar-item--multiple {
		background-color: #f98116;
		color: #fff;
		opacity: 0.8;
		margin: 0 auto;
	}
</style>
