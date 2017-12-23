<template>
	<div class="song-list">
		<ul>
			<li v-for="song in songs" class="item">
				<div class="content">
					<h2 class="name">{{song.name}}</h2>
					<p class="desc">{{getDesc(song)}}</p>
				</div>
			</li>
		</ul>
	</div>
</template>

<script>
	export default{
		props:{
			songs:{
				type:Array,
				default:[]
			}
		},
		methods:{
			getDesc(song){
				return `${song.singer}·${song.album}`
			}
		}
	}
</script>

<style scoped="scoped">
	.song-list li{
		list-style-type: none;
	}
	.item{
		list-style-type: none;
	}
	.name{
		padding-left: 0;height: 50px;line-height: 50px;font-size: 16px;
	}
	.desc{
		color: #575957;font-size: 14px;
	}
	
</style>