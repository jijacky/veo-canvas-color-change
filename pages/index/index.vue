<template>
	<view class="content">
		<!-- #ifndef MP-WEIXIN -->
		<!-- 使用示例 -->
		<view class="code-examples">
			<veo-canvas-color-change :img="img" ></veo-canvas-color-change>
            <!-- @click="myclick" -->
		</view>
		
		<!-- #endif -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
                img:''
            }
		},
		onLoad() {
		},
		methods: {
		}
	}
</script>

<style>
	.content {
		display: flex;
		height: calc(100vh - 44px);
		box-sizing: border-box;
		padding: 30rpx;
		flex-direction: column;
	}

	.code-examples {
		flex: 1;
		margin-bottom: 30rpx;
	}

	.code-examples-title {
		padding: 16rpx;
		font-size: 28rpx;
		display: block;
		border-left: 5px solid #1FC7B7;
	}

	.code-view {
		width: 100%;
		display: flex;
		flex-wrap: nowrap;
		background-color: #F1F1F1;
		margin-bottom: 10rpx;
		padding: 20rpx;
		box-sizing: border-box;
	}

	.code-text {
		font-size: 24rpx;
		white-space: nowrap;
	}

	.nav {
		padding: 20rpx;
		text-align: center;
		font-size: 26rpx;
		background-color: #F0584A;
		color: #FFFFFF;
	}
</style>
