# h5--
一个H5的微信内的活动
>活动链接：https://edu.jianxc.com/cred/index.php?m=Home&c=Tmpactive&a=term_result&id=348

![效果图查看：](http://p52hnvln4.bkt.clouddn.com/Animation.gif)

上图点开就可以看动图。或者自己复制链接去看图：http://p52hnvln4.bkt.clouddn.com/Animation.gif

###代码改进

1. 3个问题在3个页面过于冗余，可以合在一个页面通过控制js来分别显示。
2. 不用使用setTimeout可以使用callback 来实现动画后的跳转--属于对jQuery方法应用的不熟悉
```
//jQuery || 如果您希望在一个涉及动画的函数之后来执行语句，请使用 callback 函数
$("p").hide(1000,function(){
alert("The paragraph is now hidden");
});
```
