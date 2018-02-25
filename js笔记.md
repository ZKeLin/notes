[promise 实现原理剖析及实现](https://github.com/xieranmaya/blog/issues/3)  
[阮一峰的 Generator 详细介绍](http://es6.ruanyifeng.com/#docs/generator-async)
### 函数柯里化
作用：  
1，参数复用  
```
var currying = function(fn){
	var args = [].slice.call(arguments,1);
	return function(){
		var newArgs = args.concat([].slice.calll(arguments));
		return fn.apply(null,newArgs);
	} 
}
```

eg: 
``` 
var show = currying(function(){
	var args = [].slice.call(argument);
	console.log(args.join());
},'复用参数');
show('参数1','参数2'); //复用参数,参数1,参数2
show(1,2,3); //复用参数,1,2,3
```
2，延迟执行  
例子：遍历本月每天的开销并求出他们的总和  
```
var currying = function(fn){
	var args = [];
	return function(){
		if(arguments.length === 0){
			return fn.apply(this,args);
		}else{
			[].push.apply(args,arguments);
			return arguments.callee;
		}
	}
}
```
```
var cost = (function(){
	var money = 0;
	return function(){
		for(var i = 0,l = arguments.length; i < l; i++){
			money += arguments[i];
		}
		return money;
	}
})();
```
```
var costA = currying(cost);
costA(100); //没有计算
costA(200); //没有计算
console.log(costA()); //300
```
3，提前返回，例如为兼容浏览器而添加的事件方法  
```
var addEvent = (function(){
    if (window.addEventListener) {
        return function(el, sType, fn, capture) {
            el.addEventListener(sType, function(e) {
                fn.call(el, e);
            }, (capture));
        };
    } else if (window.attachEvent) {
        return function(el, sType, fn, capture) {
            el.attachEvent("on" + sType, function(e) {
                fn.call(el, e);
            });
        };
    }
})();
```
这样就不用每次用事件监听函数都进行if else 判断了。  
#### ES5的bind方法就是柯里化的实现  
```
Function.prototype.bind = function(context){
	var self = this
		,args = [].slice.call(arguments);
	return function(){
		return self.apply(context,args.slice(1))
	}
}
```

