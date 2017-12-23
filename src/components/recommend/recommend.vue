<template>
	<div class="recommend" ref="recommend">
		<div class="recommend-content" :data="disclist">
			<div>
				<div v-if="recommends.length" class="slider-wrpper" ref="sliderWrpper">
					<slider>
						<div v-for="item in recommends">
							<a :href="item.linkUrl">
								<img class="needsclick" @load="loadImage" :src="item.picUrl" />
							</a>
						</div>
					</slider>
				</div>
				
				<div class="recommend-list" ref="recommendList">
					<h1 class="list-title">热门歌单推荐</h1>
					<scroll  ref="scroll" class="recommends">
						<ul>
							<li v-for="item in disclist" class="item">
								<div class="icon">
									<img v-lazy="item.imgurl" width="60" height="60" />
								</div>
								<div class="text">
									<h2 class="name" v-html="item.creator.name"></h2>
									<p class="desc" v-html="item.dissname"></p>
								</div>
							</li>
						</ul>

					</scroll>
				</div>
				
				
			</div>
			
			<div class="loading-container" v-show="!disclist.length">
				<loading></loading>
			</div>
		</div>
	</div>
</template>

<script>

	import Slider from '../../base/slider/slider'
	import Scroll from '../../base/scroll/scroll'
	import Loading from '../../base/loading/loading'
	import {getRecommend} from '../../api/recommend'
	import {getDiscList} from '../../api/recommend'
	import {ERR_OK} from '../../api/config'
	
	export default{
		data(){
			return{
				recommends:[],
				disclist:[]
			}
		},
		created(){

			this.getDiscList()
			this._getRecommend()
		},
		mounted(){
			
			let h = window.innerHeight || document.documentElement.clientHeight || document.body.clientHeight
			//let offsetTop = this.$refs.scroll.$el.offsetTop
		
			console.log(this.$refs.recommendList)
		},
		methods:{

			
			getDiscList:function(){
				this.$ajax.get("/static/json/music.json").then((res)=>{
					this.disclist = res.data.data.list
				})
			},
			_getDiscList:function(){
				getDiscList().then((res)=>{
					//this.disclist = res.data.list
				})
			},
			_getRecommend:function(){
				getRecommend().then((res)=>{
					this.recommends = res.data.slider;
				})
			},
			loadImage(){
				if(!this.checkLoaded){
					this.$refs.scroll.refresh()
					this.checkLoaded = true
				}
				
			},
		},
		
		components:{
			Slider,
			Scroll,
			Loading
		}
	}
</script>

<style scoped="scoped">
	.list-title{
		color: #FFCD32;font-size:16px ;text-align: center;height: 50px;line-height:50px;
	}
	.item{
		display: flex;
		box-sizing: border-box;width: 90%;margin: 0 auto;margin-bottom: 15px;
	}
	.text{
		text-overflow: ellipsis;overflow: hidden;white-space: nowrap;padding-left: 10px;justify-content: center;flex: 1;
	}
	.name{
		font-size: 16px;padding-bottom: 10px;color: #FFFFFF;
	}
	.desc{
		font-size: 14px;color: dimgray;
	}
	*li{
		list-style-type: none;
	}
	.slider-wrpper{
		margin-top: 88px;
	}
	.recommends{
		height: 100%;
	}
</style>