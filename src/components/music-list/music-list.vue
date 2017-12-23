<template>
	<div class="music-list singer-detail">
		<div class="back">
			<
		</div>
		<h1 class="title" v-html="title"></h1>
		<div class="bg-image" :style="bgStyle" ref="bgImage">
			<div class="filter"></div>
		</div>
		<scroll :data="songs" class="list" ref="list">
			
				<song-list :songs="songs"></song-list>
			
		</scroll>
	</div>
</template>

<script>
	import Scroll from '../../base/scroll/scroll'
	import SongList from '../../base/song-list/song-list'
	export default{
		props:{
			bgImage:{
				type:String,
				default:''
			},
			songs:{
				type:Array,
				default:[]
			},
			title:{
				type:String,
				default:''
			}
		},
		computed:{
			bgStyle(){
				return `background-image:url(${this.bgImage})`
			}
		},
		mounted(){
			this.$refs.list.$el.style.top = `${this.$refs.bgImage.clientHeigh}px`
		},
		components:{
			Scroll,
			SongList
		}
	}
</script>

<style scoped="scoped">
	.title{
		text-align: center;
		color: #FFFFFF;height: 50px;line-height: 50px;font-size: 16px;background-color: rgba(0,0,0,0);position: absolute;width: 100%;
	}
	.back{
		height: 50px;line-height: 50px;position: absolute;left: 10px;color: #FFFFFF;font-weight: bold;font-size: 20px;font-weight: bold;
	}
	.bg-image{
		padding-top: 70%;background-size: cover;
	}
	.song-list{
		width: 90%;margin: 0 auto;color: #FFFFFF;
	}
	.list{
		overflow: hidden;height:100%;
	}
	
</style>