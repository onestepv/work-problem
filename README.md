# work-problem
整理下工作中遇到的问题

#### 1.需求： 监听input的输入，有值时，按钮高亮，反之，置灰
	
	setDisabled: function () {
	 /**
		* do something
		*/
	}
	that.reqId = requestAnimationFrame(this.setDisabled.bind(this));

	if neccesary , 
	 use cancelAnimationFrame(reqId)

	//考虑下兼容	
	var requestAnimationFrame = window.requestAnimationFrame || window.mozRequestAnimationFrame ||
	window.webkitRequestAnimationFrame || window.msRequestAnimationFrame || function (callback) { var id = window.setTimeout(callback, 1000 / 60); return id; };
	var cancelAnimationFrame = window.cancelAnimationFrame || window.mozCancelAnimationFrame || function (id) { clearTimeout(id); };
#### 2.在一个页面中，底部按钮固定，点击输入框时，发现底部按钮会被键盘顶起来（安卓手机出现）
	that.$btn = that.$rootDom.find('.sub-btn'); //底部按钮
	var winHeight = $(window).height();  //获取当前页面高度
	$(window).resize(function () {    //当调整浏览器窗口的大小时，发生 resize 事件。
		var thisHeight = $(this).height();
		if (winHeight - thisHeight > 50) {
			//当软键盘弹出，在这里面操作
			that.$btn.css("position", "static")
		} else {
			//当软键盘收起，在此处操作
			that.$btn.css("position", "absolute")
		}
	});
#### 3.发现底部按钮在输入框失焦之后，按钮点击无效（按钮好像脱离了页面），需要向下划一下页面，才能点击按钮
	Element.scrollIntoView() 可以让元素滚动到可窗口可视区域。
	focusout() 方法,使body或其任意子元素失去焦点时触发：
	that.$rootDom =======》 body
	that.$rootDom.focusout(function () {
		that.$rootDom[0].scrollIntoView(false);  //false 窗口会尽量滚动自身底部与元素底部对齐
	})
#### 4. ![image](https://github.com/xuqian1004/work-problem/blob/master/%E6%8D%95%E8%8E%B7.PNG)
	  在小程序中做搜索框的时候，想做到输入框有内容时，右边清除的icon显示，点击清空input内容，但是再真机调试时，发现iphone6下
	  input框在聚焦时，点击清除icon无效，依然是触发了input（猜想是不是input是原生组件，层级最高的问题，
	  但是input不聚焦时，可以点击清除按钮）
	  
	  最后发现最好的解决办法是：
	  外层模拟一个input框的样式，内层input icon 互不干扰（原先是icon 使用了position 强制覆盖在input上）！！！
	  这样icon的点击事件就不会有问题了
	  
	  这个bug的解决感想就是 一开始花了很多时间想怎么解决input层级高的问题，还试了层级更高的cover-image，
	  （但是出现了新的问题）这期间都没想到跳出这个层级问题的圈子_(´ཀ`」∠)_，实际上换个思路变通一下就解决了
	  
	

		
