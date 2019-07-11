<template>
	<view class="content">
		
			<button type="primary" @click="getluy">录音</button>
			<button type="primary" @click="delluy">结束</button>
			<button type="primary" @click="statrluy">播放</button>
			<audio style="text-align: left" :src="current.src" :poster="current.poster" :name="current.name" :author="current.author"
			 :action="audioAction" controls></audio>
		
	</view>
</template>

<script>
	import Recorder from 'js-audio-recorder';
	let recorder = new Recorder();
	export default {
		data() {
			return {
			current: {
				poster: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/audio/music.jpg',
				name: '致爱丽丝',
				author: '暂无',
				src: '' ,
			},
				audioAction: {
				method: 'pause'
			},
			}
		},
		onLoad() {

		},
		methods: {
			getluy() {
			recorder.start();
			// 回调持续输出时长
			// 更多的功能在文档上写了
			recorder.onprocess = function(duration) {
				console.log(duration);
			}
		
		},
		delluy() {
			recorder.stop();
		},
		statrluy() {
			recorder.flat()
			recorder.getPCM()
			var a = recorder.getWAVBlob()
			this.current.src = URL.createObjectURL(a)

		},
		}
	}
</script>

<style>
	.content {
		text-align: center;
		height: 400upx;
	}

	.logo {
		height: 200upx;
		width: 200upx;
		margin-top: 200upx;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
</style>
