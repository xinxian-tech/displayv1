<template>
  <div id="top">
    <div class="t1">
      <img :src='img'>
    </div>
    <div class="t2">Mind Band</div>
    <div class="t5">
      <img :src="img1">
    </div>
    <div class="t4">register</div>
    <div class="t3">login</div>
    
    
    <div></div>
  </div>
</template>

<script>
export default {
  name: 'card',
  data () {
    return {
      	name: 'Demo',
      	img: '../src/assets/images/2.png',
        img1: '../src/assets/images/1.jpg'
    }
  }
}
</script>

<style lang="scss" scoped>
#top {
	width: 100%;
  height: 80px;
  background-color:#ffffff;
}
#top div{
  
}
.t1{
  width: 60px;
  height: 60px;
  border-radius: 10px;
  margin: 10px 20px 10px 100px;
  overflow: hidden;
  float: left;
}
.t2{
  width: auto;
  height: 46px;
  font-size: 30px;
  line-height: 46px;
  margin: 17px 0px;
  cursor:default;
  float: left;
}
.t3{
  width: 80px;
  height: 40px;
  font-size: 20px;
  line-height: 40px;
  text-align: center;
  border-radius: 5px;
  background-color:rgba(255,255,255,0.6);
  margin: 20px 0px 20px;
  cursor:default;
  float: right;
}
.t4{
  width: 100px;
  height: 40px;
  font-size: 20px;
  line-height: 40px;
  text-align: center;
  border-radius: 5px;
  background-color:rgba(255,255,255,0.6);
  margin: 20px 0px 20px 10px;
  cursor:default;
  float: right;
}
.t5{
  width: 50px;
  height: 50px;
  border-radius: 25px;
  margin: 15px 100px 15px 30px;
  overflow: hidden;
  float: right;
}
img{
  width: 100%;
  height: 100%
}
</style>
