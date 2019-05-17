<template>
  <div id="card">
  	<header>
  		<img class="avatar" v-bind:src="user.img" v-bind:alt="user.name">
  		<p class="name">{{user.name}}</p>
  	</header>
  	<footer>
  		<input class="search" type="text" v-model="$store.state.filterKey" placeholder=" search user...">
  	</footer>
  </div>
</template>

<script>
export default {
  name: 'card',
  data () {
    return {
      user: {
      	name: 'Demo',
      	img: '../src/assets/images/1.jpg'
      }
    }
  }
}
</script>

<style lang="scss" scoped>
#card {
	padding: 12px;
  .avatar{
  	width: 40px;
  	height: 40px;
  	vertical-align: middle;/*这个是图片和文字居中对齐*/
  }
  .name {
  	display: inline-block;
  	padding: 10px;
  	margin-bottom: 15px;
  	font-size: 16px;
  }
  .search {
  	background:#a7d0e3;
  	height: 30px;
  	line-height: 30px;
  	margin-left: 5px;
  	border: 1px solid #a7d0e3;
  	border-radius: 4px;
  	outline: none;/*鼠标点击后不会出现蓝色边框*/
    color: #FFF;
  }
}
</style>
