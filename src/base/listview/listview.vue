<template>
	<scroll class="listview" :data="data" ref="listview" :listenScroll="listenScroll" @scroll="scroll">
		<ul>
			<li v-for="group in data" class="list-group" ref="listGroup">
				<h2 class="list-group-title">{{group.title}}</h2>
				<ul>
					<li @click="selectItem(item)" v-for="item in group.items" class="list-group-item">
						<img v-lazy="item.avatar" class="avatar" />
						<span class="name">{{item.name}}</span>
					</li>
				</ul>
			</li>
		</ul>
		<div class="list-shortcut" @touchstart="onShortcutTouchStart" @touchmove.stop.prevent="onShortcutTouchMove">
			<ul>
				<li v-for="(item,index) in shortcutList" :data-index = "index">{{item}}</li>
			</ul>
		</div>
	</scroll>
</template>

<script>
	import Scroll from '../scroll/scroll'
	import {getData} from '../../common/js/dom.js'
	
	const ANCHOR_HEIGHT = 18
	export default{
		created(){
			this.touch = {}
			this.listenScroll = true
		},
		data(){
			return {
				scrollY:-1,
				currentIndex:0
			}
			
		},
		props:{
			data:{
				type:Array,
				default:[]
			}
		},
		computed:{
			shortcutList(){
				return this.data.map((group)=>{
					return group.title.substr(0,1)
				})
			}
		},
		methods:{
			onShortcutTouchStart(e){
				let anchorIndex = getData(e.target,'index')
				let firstTouch = e.touches[0]
				this.touch.y1 = firstTouch.pageY
				this.touch.anchorIndex = anchorIndex
				this._scrollTo(anchorIndex)

			},
			onShortcutTouchMove(e){
				let firstTouch = e.touches[0]
				this.touch.y2 = firstTouch
				let delta = (this.touch.y2 - this.touch.y1)/ANCHOR_HEIGHT | 0
				let anchorIndex = this.touch.anchorIndex + delta
				this._scrollTo(anchorIndex)
			},
			scroll(pos){
				this.scrollY = pos.y
			},
			_scrollTo(index){
				this.$refs.listview.scrollToElement(this.$refs.listGroup[index],0)
			},
			selectItem(item){
				this.$emit('select',item)
			}
		},
		components:{
			Scroll	
		}
	}
</script>

<style scoped="scoped">
	.listview{
		position: relative;width: 100%;height: 100%;overflow: hidden;
	}
	.list-shortcut{
		position: fixed;right: 10px;z-index: 6;top:50%;transform: translateY(-50%);
	}
	.list-shortcut li{
		color: #FFFFFF;list-style-type: none;font-size: 12px;height: 18px;line-height: 18px;
	}
</style>