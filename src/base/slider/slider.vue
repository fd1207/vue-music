<template>
	<div class="slider" ref="slider">
		<div class="slider-group" ref="sliderGroup">
			<slot></slot>
		</div>
		<div class="dots">
			<span class="dota" v-for="(item,index) in dots" :class="{active:currentPageIndex===index}"></span>
		</div>
	</div>
</template>

<script>
	import BScroll from 'better-scroll'
	import { addClass } from '../../common/js/dom'
	//import 'common/js/dom' as dom
	export default{
		name: 'slider',
		data(){
			return {
				dots:[],
				currentPageIndex:0
			}
		},
		props:{
			loop:{
				type:Boolean,
				default:true
			},
			autoPlay:{
				type:Boolean,
				default:true
			},
			interval:{
				type:Number,
				default:1000
			}
		},
		mounted(){
			setTimeout(()=>{
				this._setSliderWidth()
				this._initSlider()
				this._initDots()
				if(this.autoPlay){
					this._play()
				}
			},20)
			
			window.addEventListener('resize',()=>{
				if(!this.slider){
					return
				}
				this._setSliderWidth(true)
				this.slider.refresh()
			})
		},
		methods:{
			_setSliderWidth(isResize){
				this.children = this.$refs.sliderGroup.children
				
				let width = 0
				let sliderWidth = this.$refs.slider.clientWidth
				for(let i=0;i<this.children.length;i++){
					let child = this.children[i]
					addClass(child,'slider-item')
					child.style.width = sliderWidth+"px"
					width+=sliderWidth
				}
				if(this.loop && !isResize){
					width+=2*sliderWidth
				}
				this.$refs.sliderGroup.style.width = width+"px"
			},
			_initDots(){
				this.dots = new Array(this.children.length-2)
			},
			_play(){
				let pageIndex = this.currentPageIndex+1
				if(this.loop){
					pageIndex+=1
				}
				this.timer = setTimeout(()=>{
					this.slider.goToPage(pageIndex,0,400)
				},this.interval)
			},
			_initSlider(){
				this.slider = new BScroll(this.$refs.slider,{
					scrollX:true,
					scrollY:false,
					momentum:false,
					snap:true,
					snapLoop:this.loop,
					snapThreshold:0.3,
					snapSpeed:400
				})
				this.slider.on("scrollEnd",()=>{
					let pageIndex = this.slider.getCurrentPage().pageX
					if(this.loop){
						pageIndex -= 1
					}
					this.currentPageIndex = pageIndex
					if(this.autoPlay){
						clearTimeout(this.timer)
						this._play();
					}
				})
			}
		},
		destoryed(){
			clearTimeout(this.timer)
		}
	}
</script>

<style scoped="scoped">
	.slider-group:after{
		content: " ";
		display: block;
		clear: both;
	}
	.slider-item{
		float: left;overflow: hidden;
	}
	.slider{
		position: relative;
	}
	.dots{
		position: absolute;bottom: 10px;text-align: center;width: 100%;
	}
	.dota{
		width: 10px;height: 10px;background-color: rgba(128,128,128,0.8);border-radius: 50%;display: inline-block;margin: 0 5px;
	}
	.active{
		width: 30px;border-radius: 5px;background-color: rgba(255,255,255,0.9)
	}
	
</style>