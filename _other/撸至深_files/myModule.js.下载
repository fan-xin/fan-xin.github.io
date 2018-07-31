$(function(){
  function autoSize(){var _height = $(window).height();
    $("body").css("height",_height);
  }
  autoSize();
  $(window).resize(function(){
    autoSize();
  })
});
(function(global,$,factory){
  //commonjs
  if ( typeof module === "object" && typeof module.exports === "object" ) {
    module.exports = global.document ?
      factory( global, true ) :
      function( w ) {
        if ( !w.document ) {
          throw new Error( "_Z requires a window with a document" );
        }
        return factory( w );
      };
  } else {
    //regular
    factory( global );
  }
}(typeof window !== "undefined" ? window : this,jQuery,function( window, noGlobal ){
  //构造函数_Z;
  function _Z(){
  }
  _Z.prototype.version = 1.0;
  //正则
  _Z.prototype.reg = {
    //身份证
    IDCard: /(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/,
    //手机号
    cellPhone: /^1(3|4|5|7|8)\d{9}$/,
    // 固话
    telephone: /^((0\d{2,3})-)(\d{7,8})(-(\d{3,}))?$/,
  };
  //虚拟键盘弹出界面调整
  //弹出前位置，弹出后位置,在windowresize事件中调用
  //$(window).resize(function(){
  //    openVirtualAdjust('20px','0px);
  //})
  _Z.prototype.openVirtualAdjust =  function(beloc,afloc){
    var hc = $(window).height();
    if(hc<wh){
      $('.checkInForm').css({'bottom':afloc})
    }else{
      $('.checkInForm').css({'bottom':beloc})
    }
  };
  //ajax提交动画
  _Z.prototype.showAjaxLayer = function(){
    $(".ajaxLayer").show()
  };
  _Z.prototype.hideAjaxLayer = function(){
    $(".ajaxLayer").hide()
  };
  //底部提示信息
  _Z.prototype.showTips = function(msg){
    $(".msgTips").html(msg).fadeIn(800);
    setTimeout(function(){
      $(".msgTips").fadeOut(1600);
    },2400)
  };
  //容器垂直居中
  _Z.prototype.verticalAlign = function(parobj,chlobj){
    var ph = $(parobj).height();
    var ch = $(chlobj).height();
    var mt = (ph-ch)/2;
    $(chlobj).css('marginTop',mt);
  };
  //预加载图片
  _Z.prototype.preloadImages = function(arr){
    //arr传图片路径的数组
    for(var i = 0;i<arr.length;i++){
      var img = document.createElement('img');
      img.src = arr[i]
    }
  };
  /*表单相关*/
  //记住密码功能
  _Z.prototype.remPassword = function(chk,accout,pwd,other){
    pwd=pwd||void(0);accout=accout||void(0);other=other||void(0);
    var isRem = $(chk).prop('checked')
    if(isRem){
      var uname = $(accout).val();//用户名
      var pwd = $(pwd).val();//密码
      localStorage.setItem('accout',uname);
      localStorage.setItem('pwd',pwd);
    }else{
      localStorage.removeItem('accout');
      localStorage.removeItem('pwd');
    }
  };
  //记住密码自动填充表单账户密码
  _Z.prototype.autoFillForm = function(lcaccount,lcpwd,accout,pwd){
    var accoutv = localStorage.getItem(lcaccount)
    var pwdv = localStorage.getItem(lcpwd)
    $(accout).val(accoutv);
    $(pwd).val(pwdv);
  };
  //获取验证码倒计时
  /**
   * @param getBtn->获取验证码按钮
   * @param callBack->点击回调
   * */
  _Z.prototype.countDown = function(getBtn,callBack){
    var timer = 10;
    var interVal = null;
    var _getBtn = $(getBtn);
    var _active = !_getBtn.hasClass('disabled');
    _getBtn.click(function(){
      _active = !_getBtn.hasClass('disabled');
      if(!_active){
        layer.msg('请稍后再试');
        return;
      }
      _getBtn.addClass('disabled');
      interVal = setInterval(function(){
        timer--;
        _getBtn.html(timer);
        if(timer<=0){
          clearInterval(interVal);
          _getBtn.removeClass('disabled');
          timer = 10;
          _getBtn.html('再次获取');
        }
      },1000);
      callBack&&callBack();
    });
  };
  //工具类
  _Z.prototype.util = {
    //数组取最大值
    arrmax:function(numarr){
      numarr = numarr.join(',').split(',');//拆分一位数组
      var max = Math.min.apply(null,numarr);
      return max;
    },
    //数组去重
    unique:function(arr){
      var newarr = [];
      for(var i = 0;i<arr.length;i++){
        if(newarr.indexOf(arr[i])<0){
          newarr.push(arr[i])
        }
      }
      return newarr;
    },
    //数组排序
    sortarr:function(arr){
      var len = arr.length,tmp;
      for(var i = 0;i<arr.length-1;i++){
        for(var j = 0;j<len-1-i;j++){
          if(arr[j]>arr[j+1]){
            tmp = arr[j];
            arr[j] = arr[j+1];
            arr[j+1] = tmp;
          }
        }
      }
      return arr;
    },
    //获取url参数
    getQueryString: function (name) {
      var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
      var r = window.location.search.substr(1).match(reg);
      if (r != null)return unescape(r[2]);
      return null;
    },
    //格式化日期
    formatDate: function (now) {
      if(!now)return '';
      var year = new Date(now).getFullYear();
      var month = new Date(now).getMonth() + 1 >= 10 ? new Date(now).getMonth() + 1 : '0' + (new Date(now).getMonth() + 1);
      var date = new Date(now).getDate() >= 10　? new Date(now).getDate() :　'0' + new Date(now).getDate();
      return year + "-" + month + "-" + date;
    },
    //格式化时间戳
    formatTime: function (now) {
      if(!now)return '';
      var year = new Date(now).getFullYear();
      var month = new Date(now).getMonth() + 1 >= 10 ? new Date(now).getMonth() + 1 : '0' + (new Date(now).getMonth() + 1);
      var date = new Date(now).getDate() >= 10　? new Date(now).getDate() :　'0' + new Date(now).getDate();
      var hour = new Date(now).getHours() >=10 ?  new Date(now).getHours() : '0' +  new Date(now).getHours();
      var minute = new Date(now).getMinutes() >= 10 ? new Date(now).getMinutes() : '0' + new Date(now).getMinutes();
      return year + "-" + month + "-" + date + "   " + hour + ":" + minute;
    },
    formatYear: function (now) {
      if(!now)return '';
      var year = new Date(now).getFullYear();
      return year;
    },
    formatMonth: function (now) {
      if(!now)return '';
      var year = new Date(now).getFullYear();
      var month = new Date(now).getMonth() + 1 >= 10 ? new Date(now).getMonth() + 1 : '0' + (new Date(now).getMonth() + 1);
      var date = new Date(now).getDate() >= 10　? new Date(now).getDate() :　'0' + new Date(now).getDate();
      return  month + "-" + date;
    },
    //格式化时间戳 时间
    formatTimeForH5: function (now) {
      var year = new Date(now).getFullYear();
      var month = new Date(now).getMonth() + 1 >= 10 ? new Date(now).getMonth() + 1 : '0' + (new Date(now).getMonth() + 1);
      var date = new Date(now).getDate() >= 10　? new Date(now).getDate() :　'0' + new Date(now).getDate();
      var hour = new Date(now).getHours();
      var minute = new Date(now).getMinutes();
      var second = new Date(now).getSeconds();
      return year + "-" + month + "-" + date + "T" + (hour == '0' ? '00' : hour)
        + ":" + (minute == '0' ? '00' : minute)  + ":" + (second == '0' ? '00' : second);
    },
    // 页面跳转
    goUrl: function (url) {
      window.location.href = url;
    }
  }
  //ui效果类
  _Z.prototype.ui = {
    //按钮反馈
    feedbtn:function(cls){
      var tars = document.querySelectorAll(cls);
      ;[].forEach.call(tars,function(tar){
        tar.addEventListener('mousedown',function(){
          tar.style.opacity = 0.618;
        });
        tar.addEventListener('mouseleave',function(){
          tar.style.opacity = 1;
        });
        document.addEventListener('mouseup',function(){
          tar.style.opacity = 1;
        });
      })
      ;[].forEach.call(tars,function(tar){
          tar.addEventListener('touchstart',function(){
              tar.style.opacity = 0.618;
          });
          tar.addEventListener('touchend',function(){
              tar.style.opacity = 1;
          });
          document.addEventListener('touchcancel',function(){
              tar.style.opacity = 1;
          });
      })
    },
    //水波纹效果
    waves:function(){
      //document.addEventListener('load',function(){
        var duration = 1250;
        // 样式string拼凑
        var forStyle = function(position){
          var cssStr = '';
          for( var key in position){
            if(position.hasOwnProperty(key)) cssStr += key+':'+position[key]+';';
          };
          return cssStr;
        };
        // 获取鼠标点击位置
        var forRect = function(target){
          var position = {
            top:0,
            left:0
          }, ele = document.documentElement;
          'undefined' != typeof target.getBoundingClientRect && (position = target.getBoundingClientRect());
          return {
            top: position.top + window.pageYOffset - ele.clientTop,
            left: position.left + window.pageXOffset - ele.clientLeft
          }
        };
        var show = function(event){
          var pDiv = event.target,
            cDiv = document.createElement('div');
          pDiv.appendChild(cDiv);
          var rectObj = forRect(pDiv),
            _height = event.pageY - rectObj.top,
            _left = event.pageX - rectObj.left,
            _scale = 'scale(' + pDiv.clientWidth / 100 * 10 + ')';
          var position = {
            top: _height+'px',
            left: _left+'px'
          };
          cDiv.className = cDiv.className + " waves-animation",
            cDiv.setAttribute("style", forStyle(position)),
            position["-webkit-transform"] = _scale,
            position["-moz-transform"] = _scale,
            position["-ms-transform"] = _scale,
            position["-o-transform"] = _scale,
            position.transform = _scale,
            position.opacity = "1",
            position["-webkit-transition-duration"] = duration + "ms",
            position["-moz-transition-duration"] = duration + "ms",
            position["-o-transition-duration"] = duration + "ms",
            position["transition-duration"] = duration + "ms",
            position["-webkit-transition-timing-function"] = "cubic-bezier(0.250, 0.460, 0.450, 0.940)",
            position["-moz-transition-timing-function"] = "cubic-bezier(0.250, 0.460, 0.450, 0.940)",
            position["-o-transition-timing-function"] = "cubic-bezier(0.250, 0.460, 0.450, 0.940)",
            position["transition-timing-function"] = "cubic-bezier(0.250, 0.460, 0.450, 0.940)",
            cDiv.setAttribute("style", forStyle(position));
          var finishStyle = {
            opacity: 0,
            "-webkit-transition-duration": duration + "ms", // 过渡时间
            "-moz-transition-duration": duration + "ms",
            "-o-transition-duration": duration + "ms",
            "transition-duration": duration + "ms",
            "-webkit-transform" : _scale,
            "-moz-transform" : _scale,
            "-ms-transform" : _scale,
            "-o-transform" : _scale,
            top: _height + "px",
            left: _left + "px",
          };
          setTimeout(function(){
            cDiv.setAttribute("style", forStyle(finishStyle));
            setTimeout(function(){
              //pDiv.removeChild(cDiv);//修改bug
            },duration);
          },100)
        };
        var waves = document.querySelectorAll('.waves');
        ;[].forEach.call(waves,function(tar){
          tar.addEventListener('click',function(e){
            show(e);
          },!1);
        });
        //document.querySelector('.waves').addEventListener('click',function(e){
        //    show(e);
        //},!1);
      //},!1);
    }
  };
  //amd
  if ( typeof define === "function" && define.amd ) {
    define( "_Z", [], function() {
      return _Z;
    } );
  }

  if ( !noGlobal ) {
    window._Z = new _Z();
  }
  return new _Z();
}));
