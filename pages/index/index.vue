<template>
	<view class="content">
		<view class="uni-list">
			<view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,index) in news" :key="index" 
			@tap="openinfo" :data-newid="item.post_id">
				<view class="uni-media-list">
					<image class="uni-media-list-logo" :src="item.author_avatar"></image>
					<view class="uni-media-list-body">
						<view class="uni-media-list-text-top">{{item.title}}</view>
						<view class="uni-media-list-text-bottom uni-ellipsis">{{item.ceated_at}}</view>
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
				news:[]
			};
		},
		onLoad:function(){
			uni.showLoading({
				title: '加载中...',
				mask: false
			});
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news',
				method: 'GET',
				data: {},
				success: res => {
					console.log(res);
					this.news=res.data;
					uni.hideLoading();
				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods: {
			openinfo(e) {
				var newid = e.currentTarget.dataset.newid;
				//console.log(newid);
				uni.navigateTo({
					url: '../info/info?newid='+newid
				});
			}
		},
	}
</script>

<style>
	.uni-media-list-body{
		height: auto;
	}
	.uni-media-list-text-top{line-height: 1.6em;	}
</style>
