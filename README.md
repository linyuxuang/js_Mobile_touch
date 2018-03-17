# js_Mobile_touch
web移动端上下触摸局部移动




<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no"/>
		<meta name="misapplication-tap-highlight" content="no"/>
		<meta name="HandheldFriendly" content="true"/>
		<meta name="MobileOptimized" content="320"/>

		<title></title>
		<script src="jq.js"></script>
		<style>
html,body{
    margin:0;
    padding: 0;
}
.btn{
    position: fixed;
    bottom: 0;
    width: 100%;
    padding: .5rem 0;
    background-color: pink;
    text-align: center;
    color: #fff;
    font-weight: 700;
}
.replyCeng{
    display: none;
    position: fixed;
    top:0;
    width:100%;
    height: 100vh;
    background-color: rgba(0,0,0,0.6);
    z-index: 100;
}
.replyContainer{
    background-color: #fff;
    position: absolute;
    bottom: 0;
    width: 100%;
    height: 24rem;
    text-align: center;
    overflow: hidden;
}
.replyList{
    position: absolute;
    top:3.2rem;
    width: 100%;
}
.replyTitle{
    position: absolute;
    top: 0;
    width:100%;
    padding:1.0625rem 0;
    border-bottom:1px solid #e0e0e2;
    z-index: 202;
    color: #575b61;
    font-size: .9375rem;
    font-weight: 700;
    background-color: #fff;
}
.closeReply{
    position: absolute;
    width: 1rem;
    height: 1rem;
    top: .25rem;
    right: .25rem;
    z-index: 202;
    margin: 1rem;
}
.reply-item{
    padding:.9375rem 1.625rem;
    font-size: .9375rem;
    line-height: 1.5;
    color: #666666;
    border-bottom:1px solid #e0e0e2;
}
.replyBtn{
   /* padding: 1.0625rem 1.625rem;*/

    font-size: .9375rem;
    color: #1daffa;
    font-weight: 700;
    width:100%;
    position: absolute;
    bottom: 0;
    background-color: #fff;
    z-index: 202;
    border-top: 1px solid #e0e0e2;
}
.replyBtn div{
    margin: 1.0625rem 1.625rem;
    padding: .6rem;
/*    width: 100%;*/
    border: 1px solid #1daffa;
    border-radius: .3rem;
}

		</style>
	</head>
	<body>
		<div>
    <img src="img/3.jpg" style="width:100%;height:auto;"/>
</div>
<div class="btn" onclick="replyCengShow()">button</div>
<div class="replyCeng">
    <div class="replyContainer">
        <div class="replyTitle">睡前小贴士</div>
        <img class="closeReply" src="image/close.png" />
        <div class="replyList" id="wrapper">
            <div class="reply-item" onclick="selectReply()">要注意哦，睡觉前不要吃水果，可以适当喝牛奶</div>
            <div class="reply-item">要注意哦，睡觉前不要吃水果，可以适当喝牛奶</div>
            <div class="reply-item">要注意哦，睡觉前不要吃水果，可以适当喝牛奶</div>
            <div class="reply-item">要注意哦，睡觉前不要吃水果，可以适当喝牛奶</div>
            <div class="reply-item">把黑暗的光线试想成大自然的安眠药，从而提示你的身体去大量地制造褪黑激素，这是一种能帮助人平静下来的激素。来自旧金山的专门从事焦虑和失眠的心理学家、心理学博士Steve Orma表示，在入睡前将灯关掉能提高褪黑激素的产量，这样人就会感到倦意。支持这一说法的研究有：2011年发表在《临床内分泌与代谢》期刊上的一篇研究报告表明，在黄昏时刻到睡觉之前暴露在明亮的灯光下会极大地压缩褪黑激素的产量，使人变得极其兴奋。</div>
            <div class="reply-item">把黑暗的光线试想成大自然的安眠药，从而提示你的身体去大量地制造褪黑激素，这是一种能帮助人平静下来的激素。来自旧金山的专门从事焦虑和失眠的心理学家、心理学博士Steve Orma表示，在入睡前将灯关掉能提高褪黑激素的产量，这样人就会感到倦意。支持这一说法的研究有：2011年发表在《临床内分泌与代谢》期刊上的一篇研究报告表明，在黄昏时刻到睡觉之前暴露在明亮的灯光下会极大地压缩褪黑激素的产量，使人变得极其兴奋。</div>
        </div>
        <div class="replyBtn">
            <div>管理</div>
        </div>
    </div>
</div>
<script>
function replyCengShow(){
    var startX;
    var startY;
    var moveEndX;
    var moveEndY;
    var testLeft;
    var fontHeight=parseInt($("html").css("fontSize"));
    
    $(".replyCeng").css("display","block");
    $('body').bind("touchmove",function(e){  
            e.preventDefault();  
        });
        //touchstart手指触碰屏幕
    $(".replyList").on("touchstart",function(e){
        startX = e.originalEvent.changedTouches[0].pageX,
        startY = e.originalEvent.changedTouches[0].pageY;
    });

    var replyListTop=parseInt($(".replyList").css("top"));
//  alert(replyListTop)
  //  touchmove //手指在屏幕上滑动
    $(".replyList").bind("touchmove",function(e){  
        moveEndX = e.originalEvent.changedTouches[0].pageX;
        moveEndY = e.originalEvent.changedTouches[0].pageY;
        var moveX;
        var moveY;
        moveX=moveEndX-startX;
        moveY=moveEndY-startY;

        canSeeHeight=$(".replyContainer").height()-($(".replyBtn").height()+2.125*fontHeight);
        //alert(canSeeHeight)
        hasTop= canSeeHeight <= $(this).height()+replyListTop ? true:false
        hasBottom = 3.2*fontHeight >= replyListTop ? true:false ;
        //向上滑动
        if(moveY < 0 && hasTop){
            $(".replyList").css("top",replyListTop+"px");
            replyListTop= replyListTop+moveY;
            replyListTop= canSeeHeight <= ($(this).height()+replyListTop) ? replyListTop : (-Math.abs($(this).height()-canSeeHeight));
        }
        //向下滑动
        else if(moveY > 0 && hasBottom){
            $(".replyList").css("top",replyListTop);
            replyListTop= replyListTop+moveY;
            replyListTop= 3.2*fontHeight >= replyListTop ? replyListTop : 3.2*fontHeight;
        }
    });

    $(".closeReply").unbind("click").bind("click",function(){
        $(".replyCeng").css("display","none");
        $('body').unbind("touchmove");
    });
}

</script>
	</body>
</html>
