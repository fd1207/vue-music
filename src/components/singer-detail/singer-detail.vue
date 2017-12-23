<template>
	<transition name="slide">
		<music-list :title="title" :bg-image="bgImage" :songs="songs"></music-list>

	</transition>
	
</template>

<script>
	import {mapGetters} from 'vuex'
	import {getSingerDetail} from '../../api/singer'
	import {ERR_OK} from '../../api/config'
	import {createSong} from '../../common/js/song'
	import MusicList from '../music-list/music-list'
	export default{
		data(){
			return{
				songs:[]
			}
		},
		computed:{
			title(){
				return this.singer.name
			},
			bgImage(){
				return this.singer.avatar
			},
			...mapGetters([
				'singer'
			])
		},
		created(){
			this.getDetail()
			
		},
		methods:{
			getDetail(){
				if(!this.singer.id){
					this.$router.push('/singer')
					return
				}
			
				getSingerDetail(this.singer.id).then((res) => {
					if(res.code===0){
						this.songs = this._normalizeSongs(res.data.list)
						console.log(this.songs)
					}

				})
			},
			_normalizeSongs(list){
				let ret = []
				list.forEach((item)=>{
					let {musicData} = item
					if(musicData.songid && musicData.albumid){
						ret.push(createSong(musicData))
					}
				})
				return ret
			}
		},
		components:{
			MusicList
		}
	}
</script>

<style scoped="scoped">
	.singer-detail{
		position: fixed;
		z-index: 100;
		top: 0;left: 0;right: 0;bottom: 0;background-color: #272727
	}
	.slide-enter-active,.slide-leave-active{
		transition: all 1s;
	}
	.slide-enter,.slide-leave-to{
		transform: translate3D(100%,0,0)
	}
</style>