<template>
  <div class="hello">
    <div>{{msg}}</div>
    <!-- <button onclick="changeCount(this)"></button> -->
    <button v-on:click="changeCount()">{{count}}</button>
    <p>{{count.toFixed(2)}}</p>
    <p>{{str.toLowerCase()}}</p>

    <!-- 不可以在标签中使用 -->
    <!-- <p v-bind:class="{{_color}}">{{str.toLowerCase()}}</p> -->

    <p v-bind:class="color" v-bind:style="s">{{str.toUpperCase()}}</p>
    <!-- 插值表达式不能应用在设置属性上 -->

    <ul v-html="li"></ul>

    <!-- 男女按钮 -->
    <div>{{ danger }}</div>
    <div>
      <input type="radio" name="sex" @click="danger=1" 
      :checked="danger==1">男  
      <input type="radio" name="sex" @click="danger=0" 
      :checked="danger==0">女


      <div>
        <div v-if="danger==1">♂男</div>
        <div v-if="danger==0">♀女</div>
      </div>

      <!-- 考试成绩评定 -->
      <div>考试成绩为:{{ cj }}</div>
      <div>
        <span v-if="cj>90">成绩评定A,...</span>
        <span v-else-if="cj>80">成绩评定B,...</span>
        <span v-else-if="cj>70">成绩评定C,...</span>
        <span v-else-if="cj>60">成绩评定D,...</span>
        <span v-else>成绩评定E,...</span>
      </div>


      <div>
        <span v-for="(str,i) in pf" :key="i">{{str}}</span>
      </div>
      
      <h1>点击按钮换图</h1>
      <h2>
        <button @click="changeImg('-')">上一页</button>
        <span>{{ rotation[rotationIndex].name }}</span>
        <button @click="changeImg('+')">下一页</button>
      </h2>
      <div v-show="isAlert" @click="alertHide">图片到头了!!!</div>

      <h2>
        <button @click="changeImg1(-1)">上一页</button>
        <span>{{ rotation[rotationIndex].name }}</span>
        <button @click="changeImg1(+1)">下一页</button>
      </h2>

      <br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  // 当前页面是组件页面
  // props: {
  // },
  data(){
    return{
      color:"red",
      s:"color:white;height:40px;background-color:black",
      count:0,
      msg:"当前页面是组件页面,项目是通过vue create 项目名称 创建的",
      str:"this is a new vue product",
      li:"<li>这是一个li标签</li>",
      danger: "0",
      cj:76.5,
      pf: [
        "成绩评定A,...",
        "成绩评定B,...",
        "成绩评定C,...",
        "成绩评定D,...",
      ],
      rotationIndex:0,
      rotation:[
        {id:1,"name":"波仔1","img":"1.jpg"},
        {id:2,"name":"波仔2","img":"2.jpg"},
        {id:3,"name":"波仔3","img":"3.jpg"},
        {id:4,"name":"波仔4","img":"4.jpg"},
        {id:5,"name":"波仔5","img":"5.jpg"},
        {id:6,"name":"波仔6","img":"6.jpg"},
      ],
      isAlert:false
    }
  },
  methods: {
    add(){},
    changeCount(){
      this.count += 5
    },
    changeSex(temp){
      this.danger = temp
    },
    changeImg(temp){
      if(temp == "-"){
        this.rotationIndex --;
        // 循环的逻辑
        // if(this.rotationIndex < 0){
        //   this.rotationIndex = this.rotation.length -1
        // } 

        // 走到头的逻辑
        if(this.rotationIndex <0){
          this.rotationIndex = this.rotation.length -1;
          this.isAlert=true;
          this.rotationIndex =0
          this.alertHide();
        }
      }
      if(temp == "+"){
        this.rotationIndex ++;
        // 循环的逻辑
        // if(this.rotationIndex > this.rotation.length -1){
        //   this.rotationIndex = 0
        // }
        // 走到头的逻辑
        if(this.rotationIndex > this.rotation.length -1){
          this.rotationIndex = this.rotation.length -1;
          this.isAlert=true;
          this.alertHide();
        }
      }
    },
    changeImg1(temp){
      this.rotationIndex += temp;
      if(this.rotationIndex < 0){
        this.rotationIndex = 0
      }
      if(this.rotationIndex > this.rotation.length -1 ){
        this.rotationIndex = this.rotation.length -1
      }
    },
    alertHide(){
      var that = this;
      setTimeout(function(){
        // this.isAlert = false; // this ==> window 
        that.isAlert = false;
      },1200)
    }
  }
}
</script>

<!-- 脚手架创建 -->
<!-- vue create 项目    脚手架创建  vue/cli vue.js -->

<!-- 手动创建 -->
<!-- 创建html页面 引包 创建vue对象  挂载项目  定义数据  渲染数据 -->

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
