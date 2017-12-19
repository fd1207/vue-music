<template>
	<scroll class="listview" :data="data">
		<ul>
			<li v-for="group in data" class="list-group">
				<h2 class="list-group-title">{{group.title}}</h2>
				<ul>
					<li v-for="item in group.items" class="list-group-item">
						<img :src="item.avatar" class="avatar" />
						<span class="name">{{item.name}}</span>
					</li>
				</ul>
			</li>
		</ul>
	</scroll>
</template>

<script>
	import Scroll from '../scroll/scroll'
	export default{
		props:{
			data:{
				type:Array,
				default:[]
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
</style>