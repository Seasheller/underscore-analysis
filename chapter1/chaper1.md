++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
## 了解 **_new_**  操作符。  
在js中使用new操作符可以创建一个对象。例如：  
```
function fn(a){
  //"use strict";
  this.a = a
  console.log(this.a);
}
fn(10);//10
var fun = new fn(2);//2
console.log(window.a);//10
console.log(fun.a);//2
```
我定义了一个函数 __*fn()*__, 这个函数在严格模式下会报错 __*Uncaught TypeError*__ ,因为函数中没有定义变量 __*a*__ .  
在非严格模式下，会在全局作用域下创建一个变量__*a*__,并将参数复制给__*a*__ 我们可以通过 __*window.a*__ 来观察。
而使用 __*new*__  操作符会做四件事情：  
  1. 创建一个{}  
  2. 将该对象的原型指向 __*fn()*__的原型对象  
  3. 改变 __*this*__ , __*this*__ 指向 1 中新建的{}空对象，在该对象上执行__*fn()*__函数  
  4. 如何 __*fn()*__ 函数中没有返回值,则将 1 中新建的对象返回,若有返回值,则按函数返回值返回  
所以在执行第11行代码时，fun相当于对象 __*{a:2}*__ 。

## underscore 中定义 *\_()*
  首先，我们来看看underscore中是如何定义 __*\_()*__ 的  
```
  // Create a safe reference to the Underscore object for use below.
  var _ = function(obj) {
    debugger;
    if (obj instanceof _) return obj;
    if (!(this instanceof _)) return new _(obj);
    this._wrapped = obj;
  };
```
  这里，我们看到,
