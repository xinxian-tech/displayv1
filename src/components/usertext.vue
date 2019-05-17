<template>
  <div id="uesrtext">
    <!-- <div class="btn-audio">
      <div>33</div>
        <audio id="mp3Btn">
            <source src="../src/assets/images/333.mp3" type="audio/mpeg" />
        </audio>
    </div>-->
    <div class="bq" v-if="isBq" style="padding: 20px 0px 0px 20px">
      <div
        style="width: 48px; height: 48px; float: left; font-size: 30px"
        v-for="(va, id) in emoji"
        :key="id"
        @click="sendEmoji(id)"
      >
        {{String.fromCodePoint(id)}}
        <!--img :src="'https://res.wx.qq.com/mpres/htmledition/images/icon/emotion/'+i+'.gif'"-->
      </div>
    </div>
    <div class="wait" v-if="bo">
      <div class="spinner">
        <div class="spinner-top">
          <div class="bounce2"></div>
          <div class="bounce1"></div>
          <div class="bounce2"></div>
          <div class="bounce3"></div>
          <div class="bounce1"></div>
          <div class="bounce2"></div>
          <div class="bounce3"></div>
          <div class="bounce2"></div>
          <div class="bounce3"></div>
          <div class="bounce1"></div>
          <div class="bounce3"></div>
          <div class="bounce2"></div>
          <div class="bounce1"></div>
          <div class="bounce2"></div>
          <div class="bounce3"></div>
          <div class="bounce1"></div>
          <div class="bounce2"></div>
          <div class="bounce3"></div>
          <div class="bounce2"></div>
          <div class="bounce1"></div>
          <div class="bounce2"></div>
          <div class="bounce3"></div>
          <div class="bounce2"></div>
          <div class="bounce3"></div>
          <div class="bounce1"></div>
          <div class="bounce2"></div>
          <div class="bounce1"></div>
          <div class="bounce3"></div>
        </div>
        <div class="spinner-bottom" style="margin-top:20px;">
          <div class="b1"></div>
          <div class="b2"></div>
          <div class="b3"></div>
        </div>
      </div>
    </div>
    <div style="width: 100%;height: 20%;background-color: #EEEEEE">
      <label id="realBtn" class="a" @click="isBq=false">
        <input
          type="file"
          id="fileInput1"
          name="file"
          class="mFileInput"
          style="left:-9999px;position:absolute;"
        >
        <img :src="img1">
      </label>
      <div class="a">
        <img :src="img2">
      </div>
      <div class="a" @click="isBq=!isBq">
        <img :src="img3">
      </div>
    </div>
    <!-- <div style="height: 1px"></div> -->
    <div id="biaoqing" contenteditable="true" @keyup.enter="addMessage"></div>
    <!-- <textarea  v-model="content"  style="height: 80px;width: 580px;font-size: 15px"></textarea> -->
    <div style="width: 100%;height: 45px;background-color: white;margin-top: 0px">
      <div class="send" @click="addMessage">
        <img :src="img4">
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from "vuex";
import $ from "jquery";

export default {
  name: "uesrtext",
  data() {
    return {
      isBq: false,
      bo: false,
      list: [
        "微笑",
        "撇嘴",
        "色",
        "发呆",
        "得意",
        "流泪",
        "害羞",
        "闭嘴",
        "睡",
        "大哭",
        "尴尬",
        "发怒",
        "调皮",
        "呲牙",
        "惊讶",
        "难过",
        "酷",
        "冷汗",
        "抓狂",
        "吐",
        "偷笑",
        "可爱",
        "白眼",
        "傲慢",
        "饥饿",
        "困",
        "惊恐",
        "流汗",
        "憨笑",
        "大兵",
        "奋斗",
        "咒骂",
        "疑问",
        "嘘",
        "晕",
        "折磨",
        "衰",
        "骷髅",
        "敲打",
        "再见",
        "擦汗",
        "抠鼻",
        "鼓掌",
        "糗大了",
        "坏笑",
        "左哼哼",
        "右哼哼",
        "哈欠",
        "鄙视",
        "委屈",
        "快哭了",
        "阴险",
        "亲亲",
        "吓",
        "可怜",
        "菜刀",
        "西瓜",
        "啤酒",
        "篮球",
        "乒乓",
        "咖啡",
        "饭",
        "猪头",
        "玫瑰",
        "凋谢",
        "示爱",
        "爱心",
        "心碎",
        "蛋糕",
        "闪电",
        "炸弹",
        "刀",
        "足球",
        "瓢虫",
        "便便",
        "月亮",
        "太阳",
        "礼物",
        "拥抱",
        "强",
        "弱",
        "握手",
        "胜利",
        "抱拳",
        "勾引",
        "拳头",
        "差劲",
        "爱你",
        "NO",
        "OK",
        "爱情",
        "飞吻",
        "跳跳",
        "发抖",
        "怄火",
        "转圈",
        "磕头",
        "回头",
        "跳绳",
        "挥手",
        "激动",
        "街舞",
        "左太极",
        "右太极"
      ],
      emoji: {
        0x1f620: [2.3, 6.1],
        0x1f616: [2.7, 5.8],
        0x1f615: [3.8, 3.5],
        0x1f622: [2.6, 4.2],
        0x1f61e: [2.8, 3.2],
        0x1f611: [4.8, 3.8],
        0x1f631: [4.2, 6.6],
        0x1f618: [8.1, 6.5],
        0x1f613: [2.8, 4.1],
        0x1f61b: [7.6, 6.3],
        0x1f61d: [6.7, 6.4],
        0x1f61c: [7.6, 6.7],
        0x1f602: [7.1, 6.8],
        0x1f633: [5.1, 5.7],
        0x1f62c: [4.4, 5.8],
        0x1f600: [8.4, 6.7],
        0x1f601: [5.5, 5.9],
        0x1f62d: [3.1, 5.6],
        0x1f610: [5.0, 3.9],
        0x1f614: [3.4, 3.1],
        0x1f623: [3.1, 4.8],
        0x1f60c: [7.2, 3.5],
        0x1f634: [5.7, 2.3],
        0x1f60d: [8.5, 7.1],
        0x1f60a: [7.9, 5.5],
        0x1f604: [8.2, 6.6],
        0x1f60e: [7.7, 5.0],
        0x1f60f: [6.1, 4.7],
        0x1f62b: [2.6, 5.6],
        0x1f612: [3.6, 3.7],
        0x1f629: [2.5, 5.2],
        0x1f609: [7.5, 5.4]
      },
      content: "",
      img1: "../src/assets/images/img01.png",
      img2: "../src/assets/images/img02.png",
      img3: "../src/assets/images/img03.png",
      img4: "../src/assets/images/img04.png"
    };
  },
  mounted() {
    $("#biaoqing").bind("dragover drop", function(event) {
      //prevent drag and drop
      event.preventDefault();
      return false;
    });
    $("img").on("mousedown", function(e) {
      e.preventDefault();
    });
    var $input = $("#fileInput1");
    // ①为input设定change事件
    var that = this;
    $input.change(function() {
      //    ②如果value不为空，调用文件加载方法
      if ($(this).val() != "" && that.bo != true) {
        // fileLoad(this);
        var formData = new FormData();
        //⑤获取传入元素的val
        var name = $(this).val();
        //⑥获取files
        var files = $(this)[0].files[0];
        var oFReader = new FileReader();
        oFReader.readAsDataURL(files);
        //⑦将name 和 files 添加到formData中，键值对形式
        formData.append("file", files);
        formData.append("name", name);
        oFReader.onloadend = function(oFRevent) {
          var src = oFRevent.target.result;
          $.ajax({
            url: "http://114.115.171.241:8008/emoji2mp3?emoji=%F0%9F%98%82",
            type: "GET",
            data: formData,
            cache: false,
            processData: false, // ⑧告诉jQuery不要去处理发送的数据
            contentType: false, // ⑨告诉jQuery不要去设置Content-Type请求头
            beforeSend: function() {
              //⑩发送之前的动作
              that.bo = true;
            },
            success: function(responseStr) {
              console.log(responseStr);
              //11成功后的动作
              that.bo = false;
              var filename = name;
              var index = filename.lastIndexOf(".");
              var ext = filename.substr(index + 1).toLowerCase();
              var musicType = ["mp3", "ogg", "wav"];
              var picType = [
                "bmp",
                "jpg",
                "jpeg",
                "gif",
                "psd",
                "png",
                "tiff",
                "tga",
                "eps"
              ];
              if (musicType.indexOf(ext) != -1) {
                //当文件为音频类
                that.content =
                  "<audio style='margin-top:10px;' src='" +
                  src +
                  "' controls='controls'></audio>";
                console.log(that.content);
                that.$store.commit("addMessage", that.content);
              } else if (picType.indexOf(ext) != -1) {
                //当文件为图片类
                that.content =
                  "<img style='margin-top:10px;width:100%;height:100%' src=" +
                  src +
                  " ></img>";
                that.$store.commit("addMessage", that.content);
                setTimeout(function() {
                  that.$store.commit("reply");
                }, 1000);
              } else {
                that.content = "其他文件格式未能上传";
                that.$store.commit("addMessage", that.content);
              }
            }
          });
        };
      } else {
        console.log("2");
      }
    });
  },
  methods: {
    sendEmoji(id) {
      var self = this;
      var xhr = new XMLHttpRequest();
      xhr.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
          console.log(this.response);
          self.$store.commit(
            "replyBlob",
            window.URL.createObjectURL(this.response)
          );
        }
      };
      xhr.open(
        "GET",
        "http://114.115.171.241:8008/emoji2mp3?emoji=" +
          String.fromCodePoint(id) +
          "&t=" +
          new Date().getTime()
      );
      xhr.responseType = "blob";
      xhr.send();
      /*
      $.ajax({
        url:
          "http://114.115.171.241:8008/emoji2mp3?emoji=" +
          String.fromCodePoint(id),
        type: "GET",
        cache: false,
        processData: false,
        contentType: false,
        beforeSend: function() {
          console.log("beforeSend");
        },
        success: function(response) {
          console.log("success");
          self.$store.commit("replymp3", response);
        }
      });
      */
    },
    getBq(e) {
      document.getElementById("biaoqing").focus();
      var html =
        "<img style='margin-top:5px' src='https://res.wx.qq.com/mpres/htmledition/images/icon/emotion/" +
        e +
        ".gif'>";
      var sel, range;
      if (window.getSelection) {
        // IE9 and non-IE
        sel = window.getSelection();
        if (sel.getRangeAt && sel.rangeCount) {
          range = sel.getRangeAt(0);
          range.deleteContents();
          // Range.createContextualFragment() would be useful here but is
          // non-standard and not supported in all browsers (IE9, for one)
          var el = document.createElement("div");
          el.innerHTML = html;
          var frag = document.createDocumentFragment(),
            node,
            lastNode;
          while ((node = el.firstChild)) {
            lastNode = frag.appendChild(node);
          }
          range.insertNode(frag);
          // Preserve the selection
          if (lastNode) {
            range = range.cloneRange();
            range.setStartAfter(lastNode);
            range.collapse(true);
            sel.removeAllRanges();
            sel.addRange(range);
          }
        }
      } else if (document.selection && document.selection.type != "Control") {
        IE < 9;
        document.selection.createRange().pasteHTML(html);
      }
    },
    addMessage(e) {
      var p_html = $("#biaoqing").html();
      var a = p_html.replace(/<div><br><\/div>/g, "");
      if (a != "") {
        document.getElementById("biaoqing").innerHTML = "";
        this.content = a;
        this.$store.commit("addMessage", this.content);
        this.content = "";
        this.isBq = false;
        //模拟回复
        var that = this;
        setTimeout(function() {
          that.$store.commit("reply");
        }, 1000);
      } else {
        document.getElementById("biaoqing").innerHTML = "";
        this.isBq = false;
        alert("内容不能为空");
      }
      // if (e.ctrlKey && e.keyCode ===13 && this.content.length) {
      // 	this.$store.commit('addMessage',this.content);
      // 	this.content='';
      // }
    }
  }
};
</script>

<style lang="scss" scoped>
.btn-audio {
  margin: 90px auto;
  width: 186px;
  height: 50px;
  background: #eeeeee no-repeat center bottom;
  background-size: cover;
}
::-webkit-scrollbar {
  width: 9px;
  background-color: #eeeeee;
}

/* 滚动槽 */
::-webkit-scrollbar-track {
  border-radius: 10px;
}

/* 滚动条滑块 */
::-webkit-scrollbar-thumb {
  border-radius: 10px;
  background: #bdbfc5;
}
#biaoqing {
  outline: none;
  height: 100px;
  width: 100%;
  overflow: auto;
  overflow-x: hidden;
  background-color: white;
  font-size: 15px;
  line-height: 17px;
}
#uesrtext {
  position: absolute;
  bottom: 0;
  right: 0;
  width: 100%;
  height: 30%;
  border-top: solid 1px #ddd;
  background-color: white;
  box-sizing: border-box;
  > textarea {
    padding: 10px;
    width: 100%;
    height: 100%;
    border: none;
    outline: none;
  }
}
.bq {
  width: 400px;
  height: 200px;
  border-radius: 10px;
  overflow: auto;
  /*position:fixed;
  top: 320px;
  left: 45%;*/
  position: absolute;
  bottom: 180px;
  left: 110px;
  /*margin-top: -33%;
  margin-left: 100px;*/
  background-color: white;
}
.a {
  width: 36px;
  height: 36px;
  float: left;
  margin-left: 30px;
}
img {
  width: 100%;
  height: 100%;
}
.send {
  width: 36px;
  height: 36px;
  float: right;
  margin-right: 20px;
}
textarea {
  resize: none;
}
.wait {
  width: 600px;
  height: 438px;
  background-color: rgba(190, 190, 190, 0.8);
  position: absolute;
  bottom: 180px;
}
.spinner {
  margin: 150px auto 0;
  height: 200px;
  width: 500px;
  text-align: center;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 10px;
  /*position:fixed;
  top: 200px;
  left: 41%;*/
}

.spinner-top div {
  width: 10px;
  height: 150px;
  background-color: #d73030;

  border-radius: 20px;
  display: inline-block;
  -webkit-animation: bouncedelay 3s infinite ease-in-out;
  animation: bouncedelay 3s infinite ease-in-out;
  /* Prevent first frame from flickering when animation starts */
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}
.spinner-bottom div {
  width: 10px;
  height: 10px;
  background-color: #d73030;
  border-radius: 5px;
  display: inline-block;
  -webkit-animation: bo 4s infinite ease-in-out;
}

.spinner .bounce1 {
  -webkit-animation-delay: -0.32s;
  animation-delay: -0.32s;
}

.spinner .bounce2 {
  -webkit-animation-delay: -0.16s;
  animation-delay: -0.16s;
}
.spinner-bottom .b1 {
  -webkit-animation-delay: 0s;
}
.spinner-bottom .b2 {
  -webkit-animation-delay: 1.5s;
}
.spinner-bottom .b3 {
  -webkit-animation-delay: 3s;
}
@-webkit-keyframes bo {
  0% {
    background: #d73030;
  }
  50% {
    background: #ebafaf;
  }
  100% {
    background: #d73030;
  }
}

@-webkit-keyframes bouncedelay {
  0%,
  80%,
  100% {
    -webkit-transform: scale(0);
  }
  40% {
    -webkit-transform: scale(1);
  }
}

@keyframes bouncedelay {
  0%,
  80%,
  100% {
    transform: scale(0);
    -webkit-transform: scale(0);
  }
  40% {
    transform: scale(1);
    -webkit-transform: scale(1);
  }
}
</style>
