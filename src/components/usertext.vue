<template>
  <div id="uesrtext">
    <div style="width: 100%;height: 20%;background-color: #EEEEEE">
      <label id="realBtn" class="a" >
       <input type="file" id="fileInput1" name="file" class="mFileInput" >
       <img :src="img1">
      </label>
      <div class="a"><img :src="img2"></div>
      <div class="a" @click='isBq=!isBq'><img :src="img3"></div>
    </div>
   <!--  <div id="biaoqing" contentEditable="true">sdasds<img style="width: 30px;height: 30px" src="https://res.wx.qq.com/mpres/htmledition/images/icon/emotion/0.gif">
    </div>
    <pre><img style="width: 30px;height: 30px" :src="img1"></pre> -->
    <textarea  v-model="content"  style="height: 80px;width: 580px;font-size: 15px"></textarea>
    <div style="width: 100%;height: 45px;background-color: white;margin-top: -5px" >
    <div class="send" @click='addMessage'>
      <img :src="img4">
    </div>
    </div>
  </div>
</template>

<script>
import {mapState} from 'vuex'
import $ from 'jquery'

export default {
  name: 'uesrtext',
  data () {
    return {
      isBq:true,
      list: [
        '微笑', '撇嘴', '色', '发呆', '得意', '流泪', '害羞', '闭嘴',
        '睡', '大哭', '尴尬', '发怒', '调皮', '呲牙', '惊讶', '难过',
        '酷', '冷汗', '抓狂', '吐', '偷笑', '可爱', '白眼', '傲慢',
        '饥饿', '困', '惊恐', '流汗', '憨笑', '大兵', '奋斗', '咒骂',
        '疑问', '嘘', '晕', '折磨', '衰', '骷髅', '敲打', '再见',
        '擦汗', '抠鼻', '鼓掌', '糗大了', '坏笑', '左哼哼', '右哼哼', '哈欠',
        '鄙视', '委屈', '快哭了', '阴险', '亲亲', '吓', '可怜', '菜刀',
        '西瓜', '啤酒', '篮球', '乒乓', '咖啡', '饭', '猪头', '玫瑰',
        '凋谢', '示爱', '爱心', '心碎', '蛋糕', '闪电', '炸弹', '刀',
        '足球', '瓢虫', '便便', '月亮', '太阳', '礼物', '拥抱', '强',
        '弱', '握手', '胜利', '抱拳', '勾引', '拳头', '差劲', '爱你',
        'NO', 'OK', '爱情', '飞吻', '跳跳', '发抖', '怄火', '转圈',
        '磕头', '回头', '跳绳', '挥手', '激动', '街舞', '左太极', '右太极',
      ],
      content:'',
      img1:'../src/assets/images/img01.png',
      img2:'../src/assets/images/img02.png',
      img3:'../src/assets/images/img03.png',
      img4:'../src/assets/images/img04.png',
    }
  },
  mounted(){
    var p_html = $("#biaoqing").html();
    console.log(p_html)
  },
  methods: {
    getBq(e){
       console.log(e)
    },
  	addMessage (e) {
      this.$store.commit('addMessage',this.content);
      this.content='';
  		// if (e.ctrlKey && e.keyCode ===13 && this.content.length) {
  		// 	this.$store.commit('addMessage',this.content);
  		// 	this.content='';
  		// }
  	}
  }
}

</script>

<style lang="scss" scoped>
#uesrtext {
	position: absolute;
  bottom: 0;
  right: 0;
  width: 100%;
  height: 30%;
  border-top: solid 1px #DDD;
  box-sizing: border-box;
  > textarea {
  	padding: 10px;
  	width: 100%;
  	height: 100%;
  	border: none;
  	outline: none;
  }
}
.bq{
  width: 350px;
  height: 200px;
  border-radius: 10px;
  overflow: auto;
  position:fixed;
  top: 320px;
  left: 45%;
  /*margin-top: -33%;
  margin-left: 100px;*/
  background-color:white;
}
.a{
  width: 36px;
  height: 36px;
  float: left;
  margin-left: 30px
}
img{
  width: 100%;
  height: 100%;
}
.send{
  width: 36px;
  height: 36px;
  float: right;
  margin-right: 20px
}
textarea{ 
resize:none 
} 
.mFileInput{
  left:-9999px;
  position:absolute;
}
</style>
