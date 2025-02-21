<template>
	
</template>

<script>
	import { createInnerAudioContext, InnerAudioContext} from '@/uni_modules/lime-audio-player'
	// const ctx = createInnerAudioContext()
	export default {
		data() {
			return {
				ctx: null as InnerAudioContext|null
			}
		},
		onLoad() {
			this.ctx = createInnerAudioContext()
			this.bindAudioEventHandlers()
			this.ctx!.src = 'https://web-ext-storage.dcloud.net.cn/uni-app/ForElise.mp3'
		},
		onShow() {
			if(this.ctx == null) return
			this.ctx!.src = 'https://web-ext-storage.dcloud.net.cn/uni-app/ForElise.mp3' //baseURL+"/public/weixin.mp3"
		},
		onUnload() {
			this.unbindAudioEventHandlers()
		},
		methods: {
			bindAudioEventHandlers(){
				if(this.ctx == null) return
				this.ctx!.volume = 0.8
				this.ctx!.autoplay = true
				this.ctx!.onError((res)=>{
					console.log('onError', res.errMsg)
				})
				this.ctx!.onPause((res)=>{
					console.log('onPause', res.errMsg)
				})
				this.ctx!.onPlay((res)=>{
					console.log('onPlay', res.errMsg)
				})
				this.ctx!.onSeeked((res)=>{
					console.log('onSeeked', res.errMsg)
				})
				this.ctx!.onTimeUpdate((_)=>{
					
				})
				this.ctx!.onCanplay((_)=>{
					console.log("可以播放了")
				})
				this.ctx!.onEnded((res)=>{
					console.log('res', res.errMsg)
				})
			},
			unbindAudioEventHandlers(){
				this.ctx!.offEnded()
				this.ctx!.offPause()
				this.ctx!.offPlay()
				this.ctx!.offSeeked()
				this.ctx!.offTimeUpdate()
				this.ctx!.offCanplay()
				this.ctx!.offEnded()
				this.ctx!.destroy()
			},
		}
	}
</script>

<style>

</style>
