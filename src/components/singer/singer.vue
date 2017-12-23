<template>
	<div class="singer">
		<list-view @select="selectSinger" :data="singer"></list-view>
		<router-view></router-view>
	</div>
</template>

<script>
	import Singer from '../../common/js/singer'
	import ListView from '../../base/listview/listview'
	import {mapMutations} from 'vuex'
	import {getSinger} from '../../api/singer'
	const HOT_NAME = '热门'
	const HOT_SINGER_LEN = 10
	export default{
		data(){
			return{
				singer:[]
			}
		},
		created(){
			this._getSinger()
		},
		methods:{
			selectSinger(singer){
				this.$router.push({
					path:`/singer/${singer.id}`
				})
				this.setSinger(singer)
			},
//			_getSinger:function(){
//				this.$ajax.get("/static/json/singer.json").then((res)=>{
//
//				})
//			},
			_getSinger:function(){
				getSinger().then((res)=>{
					this.singer = (this._normalizeSinger(res.data.list))
				})
			},
			_normalizeSinger(list){
				let map = {
					hot:{
						title:HOT_NAME,
						items:[]
					}
				}
				list.forEach((item,index)=>{
					if(index<HOT_SINGER_LEN){
						map.hot.items.push(new Singer({
							id:item.Fsinger_mid,
							name:item.Fsinger_name
						}))
					}
					const key = item.Findex
					if(!map[key]){
						map[key] = {
							title:key,
							items:[]
						}
					}
					map[key].items.push(new Singer({
							id:item.Fsinger_mid,
							name:item.Fsinger_name
						}))
				})
				//为了得到有序列表，我们需要处理map
				let hot = []
				let ret = []
				for(let key in map){
					let val = map[key]
					if(val.title.match(/[a-zA-Z]/)){
						ret.push(val)
					}else if(val.title === HOT_NAME){
						hot.push(val)
					}
				}
				ret.sort((a,b)=>{
					return a.title.charCodeAt(0) - b.title.charCodeAt(0)
				})
				return hot.concat(ret)
			},
			...mapMutations({
				setSinger:'SET_SINGER'
			})
		},
		components:{
			ListView
		}
	}
</script>

<style>

	.singer{
		margin-top: 88px;
	}
	.list-group-item{
		display: flex;color: #FFFFFF;width: 90%;margin: 0 auto;margin-bottom: 20px;align-items: center;
	}
	.avatar{
		width: 60px;height: 60px;border-radius: 50%;
	}
	.name{
		text-overflow: ellipsis;overflow: hidden;white-space: nowrap;padding-left: 10px;justify-content: center;flex: 1;font-size: 14px;
	}
	.list-group-title{
		color: #FFFFFF;height: 40px;line-height: 40px;background-color:#313131;padding-left: 20px;font-size: 14px;margin-bottom: 10px;
	}
	
</style>