<template>
  <div class="tab">
    <router-link tag="div" class="tab-item" to="/recommend">
      <span class="tab-link">推荐</span>
    </router-link>
    <router-link tag="div" class="tab-item" to="/singer">
      <span class="tab-link">歌手</span>
    </router-link>
    <router-link tag="div" class="tab-item" to="/rank">
      <span class="tab-link">排行</span>
    </router-link>
    <router-link tag="div" class="tab-item" to="/search">
      <span class="tab-link">搜索</span>
    </router-link>
  </div>
</template>

<script>
  export default {}
</script>

<style scoped  rel="stylesheet">

  .tab{
  	display: flex;
    height: 44px;
    line-height: 44px;

  }
    
  .tab-item{
  	flex: 1;
    text-align: center;
    color: #ffffff;
  }
      
  .tab-link{
  	padding-bottom: 5px;font-size: 15px;
  }

	.router-link-active span{
		color:#FFCD32 ;border-bottom: 3px solid #FFCD32;
	}



</style>