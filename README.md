# h5--
一个H5的微信内的活动
>活动链接：https://edu.jianxc.com/cred/index.php?m=Home&c=Tmpactive&a=term_result&id=348

![效果图查看：](http://p52hnvln4.bkt.clouddn.com/Animation.gif)

上图点开就可以看动图。或者自己复制链接去看图：http://p52hnvln4.bkt.clouddn.com/Animation.gif


###  代码改进


1. 3个问题在3个页面过于冗余，可以合在一个页面通过控制js来分别显示。
2. 不用使用setTimeout可以使用callback 来实现动画后的跳转--属于对jQuery方法应用的不熟悉
```
//jQuery || 如果您希望在一个涉及动画的函数之后来执行语句，请使用 callback 函数
$("p").hide(1000,function(){
alert("The paragraph is now hidden");
});
```

3. 请求后台的接口使用的直接就是
```
$.ajax({
        url: "{:U("term_begins")}",
        type: 'POST',
        dataType: 'json',
        data: {userName: userName, sex: sex},
        success: function(result){
            if (result.status==1) {
                window.location.href = result.url;
            }else{
                alert(result.info);
            }
        }
    });
tips:直接就使用了jQuery的ajax进行的请求    
```

### 对微信公众号/企业号的开发必备

步骤一：引入JS文件
使用微信的js-sdk能力需要引入如下文件
`<script src="https://res.wx.qq.com/open/js/jweixin-1.0.0.js"></script>`

步骤二：通过config接口注入权限验证配置[所有使用js-sdk的都需要配置一下的]
```
wx.config({
    debug: true, // 开启调试模式,调用的所有api的返回值会在客户端alert出来，若要查看传入的参数，可以在pc端打开，参数信息会通过log打出，仅在pc端时才会打印。
    appId: '', // 必填，企业号的唯一标识，此处填写企业号corpid
    timestamp: , // 必填，生成签名的时间戳
    nonceStr: '', // 必填，生成签名的随机串
    signature: '',// 必填，签名，见附录1
    jsApiList: [] // 必填，需要使用的JS接口列表，所有JS接口列表见附录2
});
```
步骤三：通过ready接口处理成功验证【config验证成功后会执行这里的内容】
```
wx.ready(function(){
    // config信息验证后会执行ready方法，所有接口调用都必须在config接口获得结果之后，config是一个客户端的异步操作，所以如果需要在页面加载时就调用相关接口，则须把相关接口放在ready函数中调用来确保正确执行。对于用户触发时才调用的接口，则可以直接调用，不需要放在ready函数中。
});
```
每一个页面都调用了，可以在代码中看到呢。

步骤四：通过error接口处理失败验证
```
wx.error(function(res){
    // config信息验证失败会执行error函数，如签名过期导致验证失败，具体错误信息可以打开config的debug模式查看，也可以在返回的res参数中查看，对于SPA可以在这里更新签名。
});
```
然而事实是我们的页面并没有处理失败。

剩下的就是接口调用了。
此处的接口调用跟微信小程序的特别类似，所以也么有问题。
