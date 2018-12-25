# work-problem
整理下工作中遇到的问题

1.需求： 监听input的输入，有值时，按钮高亮，反之，置灰
	
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

2.bind apply call

	当我们使用一个函数需要改变this指向的时候才会用到call`apply`bind
	如果你要传递的参数不多，则可以使用fn.call(thisObj, arg1, arg2 ...)
	如果你要传递的参数很多，则可以用数组将参数整理好调用fn.apply(thisObj, [arg1, arg2 ...])
	如果你想生成一个新的函数长期绑定某个函数给某个对象使用，则可以使用const newFn = fn.bind(thisObj); 
	newFn(arg1, arg2...)
	
3.写一个简单的Promise对象
		
		function aaa () {
			this.size = 2;
			this.width = 100;
			return new Promise(function (res, rej) {
				if (this.size == 1) {
					res(this.size)
				} else {
					res(this.width)
				}
			})
		}
		aaa().then(e => {console.log(e)}).catch(e => {console.log(e)})
		
4.propototy

		function aaa () {
				this.size = 2;
				this.width = 100;
		}
		aaa.prototype = {
				constructor: aaa,
				sum: function (param) {
						console.log('oops')
				}
		}
		bbb = new aaa();		
		bbb.sum();		//opps
		
5.map

	const items = [
		['name', '张三'],
		['title', 'Author']
	];

	const map = new Map();

	items.forEach(
		([key, value]) => map.set(key, value)
	);
	console.log(map)	
	console.log([...map])

	for ( let key of map.keys()) {
		console.log(key)
	}

	for (let value of map.values()) {
		console.log(value);
	}

	for (let item of map.entries()) {
		console.log(item[0], item[1]);
	}
	//或者
	for (let [key, value] of map.entries()) {
		console.log(key, value);
	}

	// 等同于使用map.entries()
	for (let [key, value] of map) {
		console.log(key, value);
	}

	var arr = [...map]    
	for (let [key, value] of arr) {
		console.log(key, value);
	}
		
