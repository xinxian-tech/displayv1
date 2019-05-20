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
          accept=".png, .jpg, .jpeg"
        >
        <img :src="img1">
      </label>
      <label id="realBtn" class="a" @click="isBq=false">
        <input
          type="file"
          id="fileInput2"
          name="file2"
          class="mFileInput"
          style="left:-9999px;position:absolute;"
          accept=".wav"
        >
        <img :src="img2">
      </label>
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

    var self = this;

    $("#fileInput2").change(function() {
      self.sendFile2();
      self.bo = true;

      setTimeout(function() {
        self.bo = false;

        var obj = $("#fileInput2")[0].files[0];
        var src = window.URL.createObjectURL(obj);
        self.content =
          "<audio style='margin-top:10px;' src='" +
          src +
          "' controls='controls'></audio>";
        self.$store.commit("addMessage", self.content);
      }, 5000);
    });

    $("#fileInput1").change(function() {
      self.sendFile();
      self.bo = true;

      setTimeout(function() {
        self.bo = false;

        var obj = $("#fileInput1")[0].files[0];
        var src = window.URL.createObjectURL(obj);
        self.content =
          "<img style='margin-top:10px;width:100%;height:100%' src=" +
          src +
          " ></img>";
        self.$store.commit("addMessage", self.content);
      }, 5000);
    });
  },
  methods: {
    sendEmoji(id) {
      this.$store.commit("addMessage", String.fromCodePoint(id));

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
    },
    sendFile() {
      const file = document.getElementById("fileInput1");
      let formData = new FormData();
      formData.append("file", file.files[0]);
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
        "POST",
        "http://114.115.171.241:8008/img2mp3?t=" + new Date().getTime()
      );
      xhr.responseType = "blob";
      xhr.send(formData);
    },
    sendFile2() {
      const file = document.getElementById("fileInput2");
      let formData = new FormData();
      formData.append("file", file.files[0]);
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
        "POST",
        "http://114.115.171.241:8008/humming2mp3?t=" + new Date().getTime()
      );
      xhr.responseType = "blob";
      xhr.send(formData);
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
