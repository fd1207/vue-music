<template>
	<div class="loading">
		<img src="../../../static/img/loading.gif" />
		<p class="desc">{{title}}</p>
	</div>
</template>

<script>
	export default{
		props:{
			title:{
				type:String,
				default:'正在载入...'
			}
		}
	}
</script>

<style scoped="scoped">
	.loading{
		width: 100%;text-align: center;position: fixed;top: 50%;transform: translateY(-50%);
	}
	.loading img{
		height: 40px;
	}
	.desc{
		line-height: 20px;
		font-size: 14px;
		color: #FFFFFF;
	}
</style>