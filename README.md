# js-work-problem（js工作中常遇到的问题总结）
## 如何判断是否为PC端 还是 移动端
```js
function goPAGE() {
  if((navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i))) {
        /*window.location.href="你的手机版地址";*/
        alert("mobile")
  }else {
    /*window.location.href="你的电脑版地址"; */
    alert("pc")
  }
}
goPAGE();
```
## 回到顶部
```js
$(".return_btnbox").click(function(){
    $('body,html').animate({scrollTop:0},500);
});
```
## 判断滚轮向上或向下移动：
移动端：
```js
var windowTop=0;//初始话可视区域距离页面顶端的距离
$(window).scroll(function() {
    var scrolls = $(this).scrollTop();//获取当前可视区域距离页面顶端的距离
    if(scrolls>=windowTop){//表示页面在向下滑动   //需要执行的操作
        windowTop=scrolls;
        console.log("向下滑动")
    }else{//表示页面在向上滑动 //需要执行的操作
        windowTop=scrolls;
        console.log("向上滑动")
    }
});
```
pc端：
```js
方式一：（不兼容火狐）
document.onmousewheel = function(e) {
    e = e || window.event;
    var wheelDelta = e.wheelDelta;
    if (wheelDelta > 0) {
        console.log("鼠标向上滚动");
        console.log(1);
    } else {
        console.warn("鼠标向下滚动");
        console.log(2);
    }
}
方式二：兼容火狐
var agent = navigator.userAgent;
if (/.*Firefox.*/.test(agent)) {
    document.addEventListener("DOMMouseScroll", function(e) {
        e = e || window.event;
        var detail = e.detail;
        if (detail > 0) {
            console.log("鼠标向下滚动");
        } else {
            console.warn("鼠标向上滚动");
        }
    });
} else {
    document.onmousewheel = function(e) {
        e = e || window.event;
        var wheelDelta = e.wheelDelta;
        if (wheelDelta > 0) {
            console.log("鼠标向上滚动");
        } else {
            console.warn("鼠标向下滚动");
        }
    }
}
```
## 一定位置显示
方式一：
```js
$(window).scroll(function(){
    var st = $(this).scrollTop();
    if(st > 100){
        $('.right_bigbox').show();
    }else{
        $('.right_bigbox').hide();
    }
});
```
方式二：
```js
$(window).scroll(function(){
    if ($(window).scrollTop()>200){
        $(".return_btnbox").fadeIn();
    }else{
        $(".return_btnbox").fadeOut();
    }
});
```
## 获取多个input选中状态：
```js
var chk_value =[];
$("input[type='checkbox']:checked").each(function(){
    chk_value.push($(this).val());
});
console.log(chk_value);
```
## 单个input选中
```js
$('input[type='checkbox']:checked'）.val()
```
## 循环获取文本内容
```js
var h3=$("h3.a");
for(i=0,len=h3.length;i<len;i++){

    if($(h3[i]).text()!==""){
        $(h3[i]).before("<em>"+$(h3[i]).text()+"</em>");
        $(h3[i]).remove();
    }
}
```
## js控制页面 
```js
window.history.go(-1);
window.location.href=“”
```
## 实现下拉框滑动效果
slideToggle([s],[e],[fn])方法

[speed],[easing],[fn]Number/String,String,Function

speed:三种预定速度之一的字符串("slow","normal", or "fast")或表示动画时长的毫秒数值(如：1000)

easing:(Optional) 用来指定切换效果，默认是"swing"，可用参数"linear"

fn:在动画完成时执行的函数，每个元素执行一次。

例子：html部分

```html
<p>这是一个段落。</p>
<button>切换 slideUp() 和 slideDown()</button>
```
js部分
```js
$(document).ready(function(){
	$("button").click(function(){
		$("p").slideToggle();
	});
  $("p").slideToggle("fast",function(){
   alert("Animation Done.");
 });
});
```
## 字符串操作

### 1.去除字符串空格
```js
/*
* 去除字符串空格 传递参数 字符串string，空格位置type（前、后、全部、前后）
* 前 before 后 after 全部 all 前后 befa
*/
    trim (str,type) {
      switch(type){
        case 'all' :
          return str.replace(/\s+/g,'');
          break;
        case 'befa' :
          return str.replace(/(^\s*)|(\s*$)/g,'');
          break;
        case 'before' :
          return str.replace(/(^s*)/g,'');
          break;
        case 'after' :
          return str.replace(/(^s*$)/g,'');
          break;
        default :
          return str;
      }
    }
    
    var str=" 123 123 3 123123 23 2 "
    console.log(this.trim(str,'all'))
```
### 2.大小写切换(字母)
```js
/*
* 大小写字母切换 传递参数 字符串string，切换类型type（1,2,3,4,5）
* 1 首字母大写 2 首字母小写 3 大小写转换 4 全部大写 5 全部小写
*/
changeCase (str,type) {
      function ToggleCase(str){
        var itemText = '';
        str.split('').forEach(
          function(item){
            if(/^([a-z]+)/.test(item)){
              itemText += item.toUpperCase();
            } else if(/^([A-Z]+)/.test(item)){
              itemText += item.toLowerCase();
            } else {
              itemText += item;
            }
          }
        )
        return itemText;
      }
      switch(type){
        case '1':
          return str.replace(/^(\w)(\w+)/,function(v,v1,v2){
            return v1.toUpperCase() + v2.toLowerCase();
          })
          break;
        case '2':
          return str.replace(/^(\w)(\w+)/,function(v,v1,v2){
            return v1.toLowerCase() + v2.toUpperCase();
          })
          break;
        case '3':
          return ToggleCase(str);
          break;
        case '4':
          return str.toUpperCase();
          break;
        case '5':
          return str.toLowerCase();
          break;
        default:
          return str;
      }
    }
    
    var str = 'abCdEFGiougFRTWRddsaikcb123456';
    alert(this.changeCase(str,'3'))
```
### 3.复制字符串
```js
/*
* 复制字符串 传递参数 字符串string，count 复制次数
*/
    repeatStr (str,count) {
      var text = '';
      for(var i=0;i < count;i++){
        text += str;
      }
      return text;
    }
    
    var str="123"
    alert(this.repeatStr(str,5))
```
### 4.字符串替换
```js
    /*
    * 字符串替换指定字符串 传递参数（字符串，被替换字符串，替换字符串），
    */
    replaceAll (str,str2,str3) {
      let raRegExp = new RegExp(str2,'g');
      return str.replace(raRegExp,str3);
    }
    
    var str="abcdkeabcsfeabc";
    var str1="abc";
    var str2="A";
    alert(this.replaceAll(str,str1,str2))
```
### 5.密码强度检测
```js
/*
* 密码强度检测 传递参数 密码字符串string，
*/
checkPwd (pwd) {
      var pwdLv = '';
      if(pwd.length >=6) {
        if(/[a-zA-Z]+/.test(pwd) && /[0-9]+/.test(pwd) && /\W+\D+/.test(pwd)) {
          var pwdLv = '强';
          return pwdLv;
        } else if(/[a-zA-Z]+/.test(pwd) || /[0-9]+/.test(pwd) || /\W+\D+/.test(pwd)) {
          if(/[a-zA-Z]+/.test(pwd) && /[0-9]+/.test(pwd)) {
            pwdLv = '中';
            return pwdLv;
          } else if(/\[a-zA-Z]+/.test(pwd) && /\W+\D+/.test(pwd)) {
            pwdLv = '中';
            return pwdLv;
          } else if(/[0-9]+/.test(pwd) && /\W+\D+/.test(pwd)) {
            pwdLv = '中';
            return pwdLv;
          } else {
            pwdLv = '弱'
            return pwdLv;
          }
        }
      } else {
        pwdLv = '弱'
        return pwdLv;
      }
    }
    
    var str="zzt910725..."
    alert(this.checkPwd(str))
```
### 6.查找字符串出现次数
```js
/*
* 查找字符串出现次数 传递参数（字符串，要查找字符串），
*/
countStr (str,str2) {
      return str.split(str2).length-1;
    }
    
    var str = 'asfsdfsblogdffsdrwblogrwrwrblogweriosfposdblogfpweproblogkwerblogmlwejsdflkblogjiouoqblognw'
    alert(this.countStr(str,'blog'))
```
## 数组操作
### 1.数组快速排序
```js
/*
* 数组快速排序 参数 数组arr
*/
quickSort (arr) {
      if(arr.length <= 1){
        return arr;
      }
      var num = Math.floor(arr.length/2);
      var numVal = arr.splice(num,1);
      var left=[];
      var right=[];
      for(var i=0;i < arr.length;i++){
        if(arr[i] < numVal){
          left.push(arr[i]);
        }else{
          right.push(arr[i]);
        }
      }
      return this.quickSort(left).concat([numVal],this.quickSort(right));
    }
    
    var arr=['1','2','1','3','4','7','1','1','9','1','1'];
    alert(this.quickSort(arr));
```
### 2.最大、最小值
```js
/*
* 数组最大、最小值 参数 数组arr，主要针对数字类型数组
*/
maxArr (arr){
      return Math.max.apply(null,arr);
    },
minArr:function(arr){
      return Math.min.apply(null,arr);
    }
    
    var arr=[1,3,5,6,7,9,12,15,17,19];
    alert(this.maxArr(arr));
    alert(this.minArr(arr));
```
### 3.和、平均值
```js
    /*
     * 数组求和、平均值 参数 数组arr，主要针对数字类型数组
    */
    sumArr:function(arr){
      var sum = 0;
      for(var i=0;i < arr.length;i++){
        sum += arr[i];
      }
      return sum;
    },
    covArr:function(arr){
      var sum=this.sumArr(arr);
      var cov=sum/arr.length;
      return cov;
    }
    
    var arr=[1,3,5,6,7,9,12,15,17,19];
    alert(this.sumArr(arr));
    alert(this.covArr(arr));
```
## 常用方法
### 获取url参数
```js
     /*
    * 获取url参数 参数 url
    */
    getUrlParmt (url) {
        url = url ? url : window.localtion.href
        var _pa = url.substring(url.indexOf('?')+1)
        var _arrs = _pa.split('&')
        var _rs = {}
        for(var i=0; i<_arrs.length;i++){
          var pos = _arrs[i].indexOf('=');
          if(pos === -1){
            continue;
          }
          var name = _arrs[i].substring(0,pos)
          var value = window.decodeURIComponent(_arrs[i].substring(pos + 1))
          _rs[name] = value
        }
      return _rs;
    }
    
    var url='http://www.baidu.com/search?id=123&username=lijian';
    console.log(JSON.stringify(this.getUrlParmt(url)));
```
### 金额大写转换
```js
    upDigit:function(n){
      var fraction = ['角','分','厘'];
      var digit = ['零','壹','贰','叁','肆','伍','陆','柒','捌','玖'];
      var unit = [['元','万','亿'],['','拾','佰','仟']];
      var head = n < 0 ? '欠人民币' : '人民币';
      n = Math.abs(n);
      var s = '';
      for(var i=0;i < fraction.length;i++){
        s += (digit[Math.floor(n*10*Math.pow(10,i))%10] + fraction[i]).replace(/零./,'');
      }
      s = s || '整';
      n = Math.floor(n);
      for(var i=0;i<unit.length;i++){
        var p = '';
        for(var j=0;j < unit[1].length && n > 0;j++){
          p = digit[n%10] + unit[1][j] + p;
          n = Math.floor(n/10);
        }
        s = p + unit[0][i] + s;
      }
      return head + s.replace(/(零.)*零元/,'元').replace(/(零.)+/g,'零').replace(/^整$/,'零元整')
    }
 ```
 ### 浏览器判断
 ```js
  browserVersion () {
      var userAgent = navigator.userAgent // 取得浏览器的userAgent字符串
      var isIE = userAgent.indexOf('compatible') > -1 && userAgent.indexOf('MSIE') > -1 // 判断是否IE<11浏览器
      var isIE11 = userAgent.indexOf('Trident') > -1 && userAgent.indexOf('rv:11.0') > -1
      var isEdge = userAgent.indexOf('Edge') > -1 && !isIE // Edge浏览器
      var isFirefox = userAgent.indexOf('Firefox') > -1 // Firefox浏览器
      var isOpera = userAgent.indexOf('Opera') > -1 || userAgent.indexOf('OPR') > -1 // Opera浏览器
      var isChrome = userAgent.indexOf('Chrome') > -1 && userAgent.indexOf('Safari') > -1 && userAgent.indexOf('Edge') === -1 && userAgent.indexOf('OPR') === -1 // Chrome浏览器
      var isSafari = userAgent.indexOf('Safari') > -1 && userAgent.indexOf('Chrome') === -1 && userAgent.indexOf('Edge') === -1 && userAgent.indexOf('OPR') === -1 // Safari浏览器
      if (isIE) {
        var reIE = new RegExp('MSIE (\\d+\\.\\d+);')
        reIE.test(userAgent)
        var fIEVersion = parseFloat(RegExp['$1'])
        if (fIEVersion === 7) {
          return 'IE7'
        } else if (fIEVersion === 8) {
          return 'IE8'
        } else if (fIEVersion === 9) {
          return 'IE9'
        } else if (fIEVersion === 10) {
          return 'IE10'
        } else {
          return 'IE6'// IE版本<7
        }
      } else if (isIE11) {
        return 'IE11'
      } else if (isEdge) {
        return 'Edge' + userAgent.split('Edge/')[1].split('.')[0]
      } else if (isFirefox) {
        return 'Firefox' + userAgent.split('Firefox/')[1].split('.')[0]
      } else if (isOpera) {
        return 'Opera' + userAgent.split('OPR/')[1].split('.')[0]
      } else if (isChrome) {
        return 'Chrome' + userAgent.split('Chrome/')[1].split('.')[0]
      } else if (isSafari) {
        return 'Safari' + userAgent.split('Safari/')[1].split('.')[0]
      }
    }
 ```
### 价钱格式化
```js
function number_format(number, decimals, dec_point, thousands_sep) {
     /*
    * 参数说明：
     * number：要格式化的数字
    * decimals：保留几位小数
    * dec_point：小数点符号
     * thousands_sep：千分位符号
    * */
   number = (number + '').replace(/[^0-9+-Ee.]/g, '');
    var n = !isFinite(+number) ? 0 : +number,
        prec = !isFinite(+decimals) ? 0 : Math.abs(decimals),
        sep = (typeof thousands_sep === 'undefined') ? ',' : thousands_sep,
        dec = (typeof dec_point === 'undefined') ? '.' : dec_point,
         s = '',
        toFixedFix = function (n, prec) {
            var k = Math.pow(10, prec);
             return '' + Math.ceil(n * k) / k;
        };
 
    s = (prec ? toFixedFix(n, prec) : '' + Math.round(n)).split('.');
     var re = /(-?\d+)(\d{3})/;
     while (re.test(s[0])) {
         s[0] = s[0].replace(re, "$1" + sep + "$2");
     }
  
     if ((s[1] || '').length < prec) {
      s[1] = s[1] || '';
        s[1] += new Array(prec - s[1].length + 1).join('0');
    }
     return s.join(dec);
}

var num=number_format(1234567.089, 2, ".", ",");//1,234,567.09

再来一个，直接舍去的办法：

function number_format(number, decimals, dec_point, thousands_sep) {
         /*
          * 参数说明：
        * number：要格式化的数字
         * decimals：保留几位小数
         * dec_point：小数点符号
        * thousands_sep：千分位符号
         * */
         number = (number + '').replace(/[^0-9+-Ee.]/g, '');
         var n = !isFinite(+number) ? 0 : +number,
  
             prec = !isFinite(+decimals) ? 0 : Math.abs(decimals),
             sep = (typeof thousands_sep === 'undefined') ? ',' : thousands_sep,
             dec = (typeof dec_point === 'undefined') ? '.' : dec_point,
             s = '',
             toFixedFix = function (n, prec) {
                 var k = Math.pow(10, prec);
                 return '' + Math.floor(n * k) / k;
             };
         s = (prec ? toFixedFix(n, prec) : '' + Math.floor(n)).split('.');
         var re = /(-?\d+)(\d{3})/;
         console.log(s)
         while (re.test(s[0])) {
            s[0] = s[0].replace(re, "$1" + sep + "$2");
         }
  
         if ((s[1] || '').length < prec) {
             s[1] = s[1] || '';
             s[1] += new Array(prec - s[1].length + 1).join('0');
         }
         return s.join(dec);
     }
    number_format(1234567.089, 2, ".", ",");//1,234,567.08

```
