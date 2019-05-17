<template>
  <div id="app">
    <top></top>
    <!-- <audioa message='../src/assets/images/333.mp3'></audioa> -->
    <div id="content">
      <div class="sidebar">
        <card></card>
        <list></list>
      </div>
      <div class="main">
        <message></message>
        <usertext></usertext>
      </div>
    </div>
  </div>
</template>

<script>
import card from './components/card.vue'
import list from './components/list.vue'
import message from './components/message.vue'
import usertext from './components/usertext.vue'
import top from './components/top.vue'

export default {
  name: 'app',
  data () {
    return {
      
    }
  },
  mounted:function() {
    this.$store.dispatch('initData');
  },
  components:{
    card,
    list,
    message,
    usertext,
    top
  }
}
</script>

<style lang="scss" scoped>
#content {
  margin: 20px auto;
  width: 800px;
  height: 600px;
  overflow: hidden;
  border-radius: 10px;
  .sidebar, .main {
    height: 100%;
  }
  .sidebar {
    float: left;
    color: #f4f4f4;
    background-color:#6EACD1;
    width: 200px;
  }
  .main {
    position: relative;
    overflow: hidden;
    background-color: rgba(255,255,255,0.9);
  }
}
</style>
