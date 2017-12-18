<template>
	<div class="recommend" ref="recommend">
		<div class="recommend-content">
			<div v-if="recommends.length" class="slider-wrpper">
				
				<slider>
					<div v-for="item in recommends">
						<a :href="item.linkUrl">
							<img :src="item.picUrl" />
						</a>
					</div>
				</slider>
			</div>
			<div class="recommend-list">
				<h1 class="list-title">热门歌单推荐</h1>
				<ul></ul>
			</div>
		</div>
	</div>
</template>

<script>

	import Slider from '../../base/slider/slider'
	export default{
		data(){
			return{
				recommends:[]
			}
		},
		created(){
			this.load()

		},

		methods:{

			load:function(){
				
				this.$ajax.get("/static/json/slider.json").then((res)=>{
		          this.recommends = res.data.data.slider;
		          //console.log(this.recommends)
		      })
			}
		},
		components:{
			Slider
		}
	}
</script>

<style scoped="scoped">
	.list-title{
		color: #FFCD32;font-size:16px ;text-align: center;height: 50px;line-height:50px;
	}
</style>