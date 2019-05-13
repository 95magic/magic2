< html >
< 头 >
< meta  http-equiv = “ Content-Type ”  content = “ text / html; charset = utf-8 ” />
< meta  name = “ viewport ”  content = “ width = device-width，hight = device-hight，minimum-scale = 1.0，maximum-scale = 1.0，ser-scalable = none ” />
< title >全屏滑稽-www.dyboy.cn </ title >

< style  type = “ text / css ” >
身体 { margin：0 ; 填充：0 ; 位置：相对 ; background-image：url（skin / images / xh.jpg）; 背景位置：中心 ; / * background-repeat：no-repeat; * /  宽度：100 ％ ; 身高：100 ％ ; 背景大小：100 ％  100 ％ ; }
#jk {
    宽度： 30 ％ ;
    位置：固定 ;
    右： 10 像素 ;
    底部： 40 像素 ;
}
</ style >

</ head >
< body  id = “ body ”  onLoad = “ init（）” >
    
< script  type = “ text / javascript ”  src = “ skin / js / threecanvas.js ” > </ script >
< script  type = “ text / javascript ”  src = “ skin / js / snow.js ” > </ script >

< script  type = “ text / javascript ” >
	var  SCREEN_WIDTH  =  窗口。innerWidth ; //
	var  SCREEN_HEIGHT  =  窗口。内心的 ;
	var容器;
	var粒子; //粒子
	VAR摄像头;
	var场景;
	var renderer;
	var starSnow =  1 ;
	var particles = [];
	var particleImage =  new  Image（）;
	// THREE.ImageUtils.loadTexture（“img / ParticleSmoke.png”）;
	particleImage。src  =  ' skin / images / ParticleSmoke.png ' ;
	
	function  init（）{
		// alert（“message3”）;
		container =  文件。createElement（' div '）; // container：画布实例;
		文件。身体。appendChild（container）;
		相机=  新 THREE.PerspectiveCamera（60，SCREEN_WIDTH  /  SCREEN_HEIGHT，1，10000）;
		相机。位置。z  =  1000 ;
		// camera.position.y = 50;
		scene =  new  THREE.Scene（）;
		场景。添加（相机）;
			
		renderer =  new  THREE.CanvasRenderer（）;
		渲染器。setSize（SCREEN_WIDTH，SCREEN_HEIGHT）;
		var material =  new  THREE.ParticleBasicMaterial（{map ： new  THREE.Texture（particleImage）}）;
			// alert（“message2”）;
		for（var i =  0 ; i <  500 ; i ++）{
			// alert（“message”）;
			particle =  new  Particle3D（材质）;
			粒子。位置。x  =  数学。random（）*  2000 - 1000 ;
			
			粒子。位置。z  =  数学。random（）*  2000 - 1000 ;
			粒子。位置。y  =  数学。random（）*  2000 - 1000 ;
			// particle.position.y = Math.random（）*（1600-particle.position.z）-1000;
			粒子。规模。x  =  粒子。规模。y  =   1 ;
			场景。添加（粒子）;
			
			粒子。推（粒子）;
		}
		容器。的appendChild（渲染器。一个DOMElement）;
		// document.addEventListener（'mousemove'，onDocumentMouseMove，false）;
		文件。addEventListener（' touchstart '，onDocumentTouchStart，false）;
		文件。addEventListener（' touchmove '，onDocumentTouchMove，false）;
		文件。addEventListener（' touchend '，onDocumentTouchEnd，false）;
		
		setInterval（loop，1000  /  60）;
		
	}
	var touchStartX;
	var touchFlag =  0 ; //储存当前是否滑动的状态;
	var touchSensitive =  80 ; //检测滑动的灵敏度;
	// var touchStartY;
	// var touchEndX;
	// var touchEndY;
	function  onDocumentTouchStart（event）{
		如果（事件。触及。长度 ==  1）{
			// event.preventDefault（）; //取消默认关联动作;
			touchStartX =  0 ;
			touchStartX =  事件。触及 [ 0 ]。pageX ;
			// touchStartY = event.touches [0] .pageY;
		}
	}
	function  onDocumentTouchMove（event）{
		如果（事件。触及。长度 ==  1）{
			// event.preventDefault（）;
			var direction =  event。触及 [ 0 ]。pageX  - touchStartX;
			如果（数学。ABS（方向）>触敏）{
				if（direction > 0）{touchFlag =  1 ;}
				否则 if（direction < 0）{touchFlag =  - 1 ;};
				// changeAndBack（touchFlag）;
			}	
		}
	}
	function  onDocumentTouchEnd（event）{
		// if（event.touches.length == 0）{
		//  	event.preventDefault（）;
		//  	touchEndX = event.touches [0] .pageX;
		//  	touchEndY = event.touches [0] .pageY;
	
		// }这里存在问题
		var direction =  event。changedTouches [ 0 ]。pageX  - touchStartX;
		changeAndBack（touchFlag）;
	}
	function  changeAndBack（touchFlag）{
		var speedX =  25 * touchFlag;
		touchFlag =  0 ;
		for（var i =  0 ; i <  粒子。长度 ; i ++）{
			颗粒[i]中。速度= 新 THREE.Vector3（speedX，- 10，0）;
		}
		var timeOut =  setTimeout（“ ; ”，800）;
		clearTimeout（timeOut）;
		var clearI =  setInterval（function（）{
			if（touchFlag）{
				clearInterval（clearI）;
				回归 ;
			};
			speedX * = 0.8 ;
			如果（数学。ABS（speedX）<= 1.5）{
				speedX = 0 ;
				clearInterval（clearI）;
			};
			
			for（var i =  0 ; i <  粒子。长度 ; i ++）{
				颗粒[i]中。速度= 新 THREE.Vector3（speedX，- 10，0）;
			}
		}，100）;
	}
	function  loop（）{
		for（var i =  0 ; i < 粒子。长度 ; i ++）{
			var particle = particles [i];
			粒子。updatePhysics（）;
			与（粒子。位置）
			{
				if（（y < - 1000）&& starSnow）{y + = 2000 ;}
				if（x > 1000）x -  = 2000 ;
				否则 如果（x < - 1000）x + = 2000 ;
				if（z > 1000）z -  = 2000 ;
				否则 如果（z < - 1000）z + = 2000 ;
			}			
		}
		相机。lookAt（场景。位置）;
		渲染器。渲染（场景，相机）;
	}
</ script >

</ body >
</ html >
