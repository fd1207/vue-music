<template>
	<div class="recommend" ref="recommend">
		<scroll ref="scroll" class="recommend-content" :data="disclist">
			<div>
				<div v-if="recommends.length" class="slider-wrpper">
					<slider>
						<div v-for="item in recommends">
							<a :href="item.linkUrl">
								<img class="needsclick" @load="loadImage" :src="item.picUrl" />
							</a>
						</div>
					</slider>
				</div>
				<div class="recommend-list">
					<h1 class="list-title">热门歌单推荐</h1>
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
				</div>
			</div>
			
			<div class="loading-container" v-show="!disclist.length">
				<loading></loading>
			</div>
		</scroll>
	</div>
</template>

<script>

	import Slider from '../../base/slider/slider'
	import Scroll from '../../base/scroll/scroll'
	import Loading from '../../base/loading/loading'
	//import {getRecommend} from 'api/recommend'
	//import {ERR_OK} from 'api/config'
	
	export default{
		data(){
			return{
				recommends:[],
				disclist:[]
			}
		},
		created(){

			this.load()
			this.getDiscList()
		},

		methods:{

			load:function(){
				
				this.$ajax.get("/static/json/slider.json").then((res)=>{
		          this.recommends = res.data.data.slider;
		          //console.log(this.recommends)
		      })
			},
			getDiscList:function(){
				this.$ajax.get("/static/json/music.json").then((res)=>{
					console.log(res.data.data.list)
					this.disclist = res.data.data.list
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
</style>