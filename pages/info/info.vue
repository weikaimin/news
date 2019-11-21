<template>
	<view class="content">
		<view class="title">{{title}}</view>
		<view class="art-content">
			<rich-text class="richText" :nodes="stringsNews"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title:'',
				stringsNews:''
			}
		},
		onLoad:function(e){
			console.log(e);
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news/36kr/'+e.newid,
				method: 'GET',
				data: {},
				success: res => {
					console.log(res);
					this.title=res.data.title;
					this.stringsNews=res.data.content;
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style>
.content{padding: 10upx 2%; width: 96%;flex-wrap: wrap;}
.title{line-height: 2em; font-weight:700 ; font-size: 38upx;text-shadow: 1upx 1upx 0upx #F0AD4E;}
.art-content{line-height: 2em;}
</style>
