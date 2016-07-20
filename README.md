# Carousel-Demo
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>轮播</title>
<link rel="stylesheet" type="text/css" href="css/css.css"/>
<script type="text/javascript" src="js/jquery-1.12.0.min.js"></script>
<script type="text/javascript">

$(function(){
	
	var i=0;
	var clone=$(".banner .img li").first().clone();
	$(".banner .img").append(clone);	
	var size=$(".banner .img li").size();	
	for(var j=0;j<size-1;j++){
		$(".banner .num").append("<li></li>");
	}
	$(".banner .num li").first().addClass("on");
	
	
	/*鼠标划入圆点*/
	$(".banner .num li").hover(function(){
		var index=$(this).index();
		i=index;
		$(".banner .img").stop().animate({left:-index*550},500)	
		$(this).addClass("on").siblings().removeClass("on")		
	})
	
	
	/*自动轮播*/
	var t=setInterval(function(){
		i++;
		move()
	},2000)
	
	
	/*对banner定时器的操作*/
	$(".banner").hover(function(){
		clearInterval(t);
	},function(){
		t=setInterval(function(){
			i++;
			move()
		},2000)
	})
	
	
	/*向左的按钮*/
	$(".banner .btn_l").click(function(){
		i++
		move();	
	})
	
	
	/*向右的按钮*/
	$(".banner .btn_r").click(function(){
		i--
		move()				
	})
		
	
	function move(){
		
		if(i==size){
			$(".banner  .img").css({left:0})			
			i=1;
		}
		
		
		if(i==-1){
			$(".banner .img").css({left:-(size-1)*550})
			i=size-2;
		}
		
		$(".banner .img").stop().animate({left:-i*550},500)	
		
		if(i==size-1){
			$(".banner .num li").eq(0).addClass("on").siblings().removeClass("on")	
		}else{		
			$(".banner .num li").eq(i).addClass("on").siblings().removeClass("on")	
		}
		
			
	}	
	
})

</script>
</head>

<body>
<div class="banner">
	<ul class="img">
    	<li><a href="#"><img src="images/1.jpg"></a></li>
        <li><a href="#"><img src="images/2.jpg"></a></li>
        <li><a href="#"><img src="images/3.jpg"></a></li>
        <li><a href="#"><img src="images/4.jpg"></a></li>
    </ul>
    
    <ul class="num">    	
    </ul>
    
    <div class="btn btn_l">&lt;</div>
    <div class="btn btn_r">&gt;</div>

</div>

</body>
</html>
