<template>
	<transition name="slide">
		<div class="singer-detail">
			
		</div>
	</transition>
	
</template>

<script>
	import {mapGetters} from 'vuex'
	import {getSingerDetail} from '../../api/singer'
	import {ERR_OK} from '../../api/config'
	export default{
		computed:{
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
					console.log(res)

				})
			}
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