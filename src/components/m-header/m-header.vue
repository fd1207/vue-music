 <template>
  <div class="m-header">
    <div class="icon"></div>
    <h1 class="text">Chicken Music</h1>
    <router-link tag="div" class="mine" to="/user">
      <i class="icon-mine"></i>
    </router-link>
  </div>
</template>

<script>
  export default {}
</script>

<style scoped rel="stylesheet">
  

	.m-header{
	  position: relative;
	  height: 44px;
	  text-align: center;
	  font-size: 15px;
	  color: #FFCD32;
	}
    
    .icon{
      display: inline-block;
      vertical-align: top;
      margin-top: 6px;
      width: 30px;
      height: 32px;
      margin-right: 9px;
      background-size: contain;
      background-image: url(../../common/image/default.png);
      background-repeat: no-repeat;
      background-position: center;
      
    }
      
    .text{
      display: inline-block;
	  vertical-align: top;
	  line-height: 44px;
	  font-size: 20px;
    }
      
    .mine{
      position: absolute;
	  top: 0;
	  right: 0;
    }
      
    .icon-mine{
      display: block;
      padding: 12px;
      font-size: 20px;
    }
        
</style>