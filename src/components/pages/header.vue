<template>
 <div class="container-fluid" style="margin-bottom: 50px">
   <div class="row" >
     <nav class="navbar" role="navigation" style="background-color:#169f14 ">
       <div class="container">
         <div class="navbar-header">
           <a class="navbar-brand" href="#">农村社会化公共服务系统</a>
         </div>
         <div class="pull-right">
           <ul class="nav navbar-nav">
             <li v-if="userName!==''" style="margin-right: 20px"><h4>欢迎您！{{userName}}</h4></li>
             <li v-if="userName!==''" class="welcome"><img src="../../../static/images/play.png" alt="" class="img-circle img-responsive">
             <ul class="welcome-option">
               <li><a href="">修改密码</a></li>
               <li><a href="">退出登录</a></li>
             </ul>
             </li>
             <li  v-if="userName==''"><a href="#" data-toggle="modal" id="submitData" data-target="#myModal" v-on:click="creatCode()">登录</a></li>
             <!-- 模态框（Modal） -->
             <div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel"
                  aria-hidden="true">
               <div class="modal-dialog">
                 <div class="modal-content">
                   <div class="modal-header">
                     <button type="button" class="close" data-dismiss="modal" aria-hidden="true">
                       &times;
                     </button>
                     <h4 class="modal-title" id="myModalLabel" style="text-align: center" >
                       登录
                     </h4>
                   </div>
                   <div class="modal-body">
                     <div style="padding: 20px 100px 10px;">
                       <form class="bs-example bs-example-form" role="form">
                         <div class="input-group">
                           <span class="input-group-addon"><i class="glyphicon glyphicon-user"></i></span>
                           <input type="text" class="form-control" placeholder="用户名" v-model="name"
                                  v-on:blur="validactorName()">
                           <span class="btn glyphicon glyphicon-remove form-control-feedback"
                                 v-on:click="clearName()"></span>
                         </div>
                         <span style="color: #761c19">{{namedis}}</span>
                         <br>
                         <div class="input-group">
                           <span class="input-group-addon"><i class="glyphicon glyphicon-lock"></i></span>
                           <input type="password" class="form-control" PLACEHOLDER="密码" v-model="pass"
                                  v-on:blur="validactorNamePass()"><span
                           class="btn glyphicon glyphicon-remove form-control-feedback"
                           v-on:click="clearPass()"></span>
                         </div>
                         <span style="color: #761c19">{{passdis}}</span>
                         <br>
                         <div class="input-group">
                           <span class="input-group-addon" ><div v-model="checkCode">{{checkCode}}</div></span>
                           <input type="text" class="form-control" placeholder="验证码" v-model="checkPass"
                                  v-on:blur="validactorNameCkeckPass()">
                           <span style="padding: 0 0" class="input-group-addon">
                              <a style="padding: 0 0;margin: 0 0 " class="btn btn-xs btn-success"
                                 v-on:click="creatCode()">换一张</a></span>
                         </div>
                         <span style="color: #761c19">{{codedis}}</span>
                         <div style="margin-top: 10px">
                           <button type="button" class="btn btn-default" data-dismiss="modal">关闭
                           </button>
                           <button type="button" class="btn btn-primary pull-right"  v-on:click="submitLogin()" >
                             登录
                           </button>
                         </div>
                       </form>
                     </div>
                   </div>
                 </div><!-- /.modal-content -->
               </div><!-- /.modal -->
             </div>
             <li  v-if="userName==''"><a href="#" data-toggle="modal" data-target="#mymodal-data" v-on:click="creatCode()">注册</a></li>
             <div class="modal" id="mymodal-data" tabindex="-1" role="dialog" aria-labelledby="mySmallModalLabel" aria-hidden="true">
               <div class="modal-dialog">
                 <div class="modal-content">
                   <div class="modal-header">
                     <button type="button" class="close" data-dismiss="modal">
                       <span aria-hidden="true">×</span>
                       <span class="sr-only">Close</span>
                     </button>
                     <h4 class="modal-title" style="text-align: center">注册</h4>
                   </div>
                   <div class="modal-body">
                     <div style="padding: 20px 100px 10px;">
                       <form class="bs-example bs-example-form" role="form">
                         <div class="input-group">
                           <span class="input-group-addon"><i class="glyphicon glyphicon-user"></i></span>
                           <input type="text" class="form-control" placeholder="用户名" v-model="name"
                                  v-on:blur="validactorName()">
                           <span class="btn glyphicon glyphicon-remove form-control-feedback"
                                 v-on:click="clearName()"></span>
                         </div>
                         <span style="color: #761c19">{{namedis}}</span>
                         <br>
                         <div class="input-group">
                           <span class="input-group-addon"><i class="glyphicon glyphicon-lock"></i></span>
                           <input type="password" class="form-control" PLACEHOLDER="密码" v-model="pass"
                                  v-on:blur="validactorNamePass()"><span
                           class="btn glyphicon glyphicon-remove form-control-feedback"
                           v-on:click="clearPass()"></span>
                         </div>
                         <span style="color: #761c19">{{passdis}}</span>
                         <br>
                         <div class="input-group">
                           <span class="input-group-addon"><i class="glyphicon glyphicon-lock"></i></span>
                           <input type="password" class="form-control" PLACEHOLDER="确认密码" v-model="apass"
                                  v-on:blur="validactorNameaPass()"><span
                           class="btn glyphicon glyphicon-remove form-control-feedback"
                           v-on:click="clearaPass()"></span>
                         </div>
                         <span style="color: #761c19">{{apassdis}}</span>
                         <br>
                         <div class="input-group">
                           <span class="input-group-addon" ><div v-model="checkCode">{{checkCode}}</div></span>
                           <input type="text" class="form-control" placeholder="验证码" v-model="checkPass"
                                  v-on:blur="validactorNameCkeckPass()">
                           <span style="padding: 0 0" class="input-group-addon">
                              <a style="padding: 0 0;margin: 0 0 " class="btn btn-xs btn-success"
                                 v-on:click="creatCode()">换一张</a></span>
                         </div>
                         <span style="color: #761c19">{{codedis}}</span>
                         <div style="margin-top: 10px">
                           <button type="button" class="btn btn-default" data-dismiss="modal">关闭
                           </button>
                           <button type="button" class="btn btn-primary pull-right">
                             注册
                           </button>
                         </div>
                       </form>
                     </div>
                   </div>
                 </div>
               </div>
             </div>
             <li><a href="#">管理平台登录</a></li>
           </ul>
         </div>
       </div>
     </nav>
   </div>
   <div class="row">
     <div class="container">
       <div class="row">
         <div class="col col-md-2 col-xs-2 col-sm-2" style="padding-left: 0"><a href="#">
           <img src="static/images/logo.png" class="img-responsive" alt=""></a></div>
         <div class="col col-md-8 col-xs-8 col-lg-8" style="margin-top: 20px">
           <div class="button-group" style="padding-left: 0;display: inline">
             <span style="margin-right: 5px;"> <router-link to="/"><a  class="btn btn-success" >首页</a></router-link> </span>
             <span style="margin-right: 5px;">  <router-link to="/butie"><a class="btn btn-success" >政策补贴</a></router-link> </span>
             <span style="margin-right: 5px;"><a href="/hezuoshe" class="btn btn-success" >合作社运营</a> </span>
             <span style="margin-right: 5px;"><a href="/nongji" class="btn btn-success" >实用农技</a> </span>
             <span style="margin-right: 5px;"><a href="/guandian" class="btn btn-success" >农合观点</a> </span>
             <span style="margin-right: 5px;"><a href="/xueyuan" class="btn btn-success" >农合学院</a> </span>
             <span style="margin-right: 5px;"><a href="/shehuihua" class="btn btn-success" >社会化服务</a> </span>
             <span style="margin-right: 5px;"><a href="/kuaixun" class="btn btn-success" >农业快讯</a> </span>
           </div>
         </div>
         <div class="col col-md-2" style="margin-top: 20px">
           <span style="/*margin-right: 30px;*/ float: top">
               <div class="input-group">
                           <input type="text" class="form-control" PLACEHOLDER="请输入搜索内容">
               <span class="input-group-addon"><i class="glyphicon glyphicon-search"></i></span>
                 </div>
             </span>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>

<script>
  import Vue from 'vue'
  import service from '@/components/service/serviceDetils.vue'
  Vue.use(service)
    export default {
        name: "header",
      data: function () {
        return {
          name: '',
          pass: '',
          checkPass: '',
          message: '',
          passdis: '',
          codedis: '',
          checkCode: '',
          namedis:'',
          menu:'',
          apass:'',
          apassdis:'',
          userName:'admin'
        }
      },
      methods: {
        clearName: function () {
          this.name = ''
        },
        clearPass: function () {
          this.pass = ''
        },
        clearaPass: function () {
          this.apass = ''
        },
        validactorName:function () {
          if (this.name===''){
            this.namedis='用户名不能为空！'
          }else{
            if(this.name.length>6){
              this.namedis='用户名长度不能超过6位'
            }else {
              this.namedis=''
            }
          }
        },
        validactorNamePass: function () {
          if (this.pass===''){
            this.passdis='密码不能为空！'
          }else{
            if(this.pass.length<6||this.pass.length>15){
              this.passdis='密码长度不能小于6位且不能大于15位'
            }else {
              this.passdis=''
            }
          }
        },
        validactorNameaPass: function () {
          if (this.apass!==this.pass) {
            this.apassdis = '两次输入密码不一致！请核对'
          }
        },
        validactorNameCkeckPass: function () {
          if(this.checkCode.length==0){
            this.codedis='请输入验证码！'
          }else{
            console.log(this.checkCode+":"+this.checkPass)
            if ((this.checkCode.replace(" ","").trim().toLocaleLowerCase())==this.checkPass.trim().toLocaleLowerCase()){
              this.codedis='验证码不正确！'
              this.$options.methods.creatCode()
            }else{
              //提交
            }
          }
        },
        creatCode: function () {
          var code = "";
          var codeLength = 4;//验证码的长度
          var random = new Array(0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R',
            'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z');//随机数
          for (var i = 0; i < codeLength; i++) {
            //循环操作
            var index = Math.floor(Math.random() * 36);//取得随机数的索引（0~35）
            code += " " + random[index];//根据索引取得随机数加到code上
          }
          this.checkCode = code;//把code值赋给验证码
          // console.log(this.checkCode)
        },
        submitLogin:function(){
          service.methods.login(this,this.pass,this.name);
        }
      }
    }
</script>

<style scoped>
  nav {
    font-weight: bold;
  }

  .footer {
    background-color: #238129;
    margin-top: 30px;
  }

  .container-fluid {
    margin-right: 0;
    margin-left: 0;
  }
  .glyphicon-search{
    cursor: pointer;
  }

  .glyphicon-remove {
    color: #761c19;
    pointer-events: auto;
  }

  .glyphicon-remove :hover {
    cursor: pointer;
  }

  .navbar-inverse {
    background-color: #238129;
    border: none;
  }

  .navbar-inverse .navbar-nav > li > a {
    color: #ffffff;
  }

  .footer {
    list-style: none;

  }

  .navbar-inverse .navbar-brand {
    color: #ffffff;
  }

  .modal-header {
    background-color: #238129;
  }

  a {
    text-decoration: none;
    color: #fff;
  }

  ul {
    list-style: none;
    border: none;
  }

  h4 {
    color: #ffffff;
  }

  .footer ul li {
    margin-top: 10px;
  }

  li {
    word-break: break-all;
    word-wrap: break-word;
  }

  li {
    width: auto;
  }

  #menu li a :hover {
    color: #fff;
    border-radius: 5px;
    background-color: #1cba9d;
  }
  .nav > li > a:hover, .nav > li > a:focus {
    text-decoration: none;
   border: 1px  #1cba9d;
    border-radius: 5px;
    background-color: #238129;
  }
  .welcome-option{
    list-style: none;
   display: none;
    z-index: 9999;
    position: absolute;
    background-color: rgba(22,159,20,0.8);
    min-width: 120px;
    box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.5);
    padding: 12px 16px;
    margin-left: -50px;
  }
  .welcome-option li{
    text-align: center;
    margin-top: 10px;
    margin-bottom: 10px;
  }
  .welcome-option li a:hover{
    background-color: #169f14;
    border-radius: 10px;
    padding: 8px 8px;
  }
  .welcome img{
    height: 50px;
    width: 50px;
    z-index: 0;
    position: relative;
  }
  .welcome:hover .welcome-option{
    display: block;
  }
</style>
