<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	image {

		width: 100%;
	}

	button {
		margin: 50rpx;
	}

	.imgs {
		display: flex;
		justify-content: center;
		flex-direction: column;
		align-items: center;
		height: 100%;
		font-size: 18rpx;
	}

	.title {
		font-size: 35rpx;
		text-align: center;
		font-weight: bold;
	}
</style>
