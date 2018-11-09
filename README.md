# ES6 笔记

ES6学习笔记

> 注：此笔记是我在主要用Swift语言开发，对比整理的一些我感觉常用的功能特性点，匆匆忙忙，粗粗浅浅，以偏概全，仅自以为容易混淆和类比以及不同的知识点。

## 目 录
* [**var let const**](#var-let-const)
* [**解构赋值**](#解构赋值)
* [**函数**](#函数)

## var let const

* **var let 区别**

  var 在以下这样的代码块里依然是全局变量，但是 let 在里面是局部变量。
  
  ```js
  {
      var a = 1;
      let b = 2;
  }
  //输出: 1
  console.log(a);
  // 报错！
  console.log(b);
  ```
  
  在 function 里面，var 和 let 则都不可取到，其声明都是以局部变量呈现，在我看来它们都是一样的。
  
  ```js
  function func() {
      var a = 1;
      a = 3;
      //输出 3
      console.log(a);
      let b = 2;
      b = 4;
      //输出 4
      console.log(b);
  }
  func();
  // 报错！
  console.log(a);
  // 报错！
  console.log(b);
  ```
  
  且 var 命令存在 “变量提升”，也就是只要用 var 定义了变量，就算是在声明之前引用它，都不会报错；但是对 let 来说，它就很安全了，在定义之前的引用，都会报错！
  
  ```js
  //undefined
  console.log(a);
  var a = 1;

  // 报错！
  console.log(b);
  let b = 1;
  ```
  
  **总结：**现在我还不知道多文件全局变量中怎么声明，但是在单文件中，一个 let 声明就足够了！只要在代码块里，let 就是无敌的，在代码块外，let 什么都不是。

* **const**

  它就是声明常量用的，注意规范：**常量全部用大些字母表示**。
  
  ```js
  const PI = 3.14159;
  // 报错！
  PI = "what?";
  ```
  
  但是 const 也仅仅能保证
  
* **对比语言**
  * **Swift**

     在 Swift 中声明变量的方法只有 var 属性，这个 var 在单文件中，其作用就是ES6中的 let ！
         
     而 ES6 中的 const，则是声明常量的方法，作用和 Swift 里的 let 一摸一样。

## 解构赋值

* **什么是解构赋值？**

  按照一定模式，对变量赋值。JS支持数组、对象的解构赋值。
  
  ```js
  let [a, b, c] = [1, 2, 3];
  //输出：1 2 3
  console.log(a, b, c)
  ```
  
  ```js
  let {a, b} = {a: "a", b: "b"}
  //输出：a b
  console.log(a, b)
  ```
  
* **字符串的解构赋值**

  可以直接用字符串去映射一个数组。
  
  ```js
  let [a, b, c] = "hello"
  // 输出：h e l
  console.log(a, b, c)
  ```
  
* **对比语言**

    * **Swift**

      swift中的解构赋值体现在元祖上面，其他的嘛，就没有JS这么宽泛了。
      
      
## 函数

* **函数参数默认值**
  
  ES6提供了函数默认值，所以这样一个函数的写法为：
  
  ```js
  function hello(a, b = "b") {
      console.log(a);
      console.log(b);
  }
  //输出：a
  //     b
  hello("a")
  ```
  
* **函数的 length 属性**

  函数的 length 返回参数的个数，但是有默认值的参数却不算。
  
  举个🌰
  
  ```js
  let f = function (a, b, c = 0) {};
  console.log(f.length);
  //这样虽然不会报错，但也不会改变length的值
  f.length = 5;
  console.log(f.length);
  ```
  
* **函数的 rest 参数**

  函数的 rest 参数允许函数传入多个参数。
  
  ```js
  function add(...values) {
      let sum = 0;

      for (const val of values) {
        sum += val;
      }

      return sum;
  }
  //输出：6
  console.log(add(1, 2, 3));
  ```
  
* **箭头函数**

  ES6出现的一种表现函数的新方式，箭头函数：
  
  ```js
  let f = v => v;
  //等同于
  let f = function (v) { return v };
  
  let f = (a, b) => a + b;
  //等同于
  let f = function (a, b) { return a + b; }
  ```
  
  所以，下面这么写也是可以的
  
  ```js
  let f = (a, b) => {
      a += 1;
      b += 1;
      return a + b;
  }
  //输出：5
  console.log(f(1, 2));
  ```

* **this**

  this 据说是一个很让人搞糊涂的东西，其修饰的对象往往是上下文中的对象。
  
  **第一个实验：**
  
  我看了很多博客写的 this 能够取到顶层的东西，但是我自己实验，发现并不能，比如：
  
  ```js
  let a = 10;
  function helloA() {
      this.a++;
      console.log(this.a);
  }
  //输出 NaN
  helloA();
  ```
  
  > 或许是我运行环境的原因，或是 ES5 和 ES6 对 `this` 的指向改变了？感觉后者的可能小。
  
  **第二个实验**
  
  为了验证 this 是否能够取到上下文的内容，对 ES5 的便捷函数 和 ES6 的箭头函数 做了下实验：
  
  ```js
  function helloB() {
      this.b = 10;
      let func = function() {
          this.b++;
          console.log(this.b);
      };
      func();
  }
  //输出：11
  helloB();
  ```
  
  看来能够取到 `helloB` 块区里的 `this.b`，如果之前 `this.b = 10;` 这条语句用 `let b = 10;`，那么最后输出的结果就为 `NaN` 了。So, why? 我也不知道为什么这个样子，我以为替换语句也依然可以引用到呢。奇怪奇怪。
  
  接下来是 ES6 的箭头函数测试：
  
  ```js
  function helloC() {
      this.c = 10;
      let func = () => {
          this.c++;
          console.log(this.c);
      };
      func();
  }
  //输出：11
  helloC();
  ```
  
  OK，和上面得到的结果一样，那么继续替换 `this.c = 10;` 为 `let c = 10;` 实验呢，最后输出的结果也为 NaN 了。
  
  所以这个实验下来，真的有些云里雾里，`this` 的意义何在，我全程用 `let` 去定义，结果也是一样的……
  
  **第三个实验**
  
  这个实验是对对象进行的实验，同样对便捷函数和箭头函数做了测试。
  
  先来便捷函数：
  
  ```js
  var obj2 = {
      ab: 1,
      func: function() {
          this.ab++;
          console.log(this.ab);
      }
  };
  //输出：2
  obj2.func()
  ```
  
  OK，用 `this` 确实取到了对象里的 `ab` 变量。
  
  再来箭头函数：
  
  ```js
  var obj1 = {
      ab: 1,
      func: () => {
          this.ab++;
          console.log(this.ab);
      }
  };
  //输出：NaN
  obj1.func();
  ```
  
  So, WTF, again?
  
  好吧，到这做了三个实验已经 萌萌哒 了，至于书里还有对 `this` 各种情况下的各种研究，好了，够了，I'm done here. 🙌
  
* **双冒号运算符**

  ‼️
  
  书上这里内容太少，理解不透彻，先留在这 😓
  
* **尾调**

  JS 的尾递归，只保留一个调用记录，减少了复杂度和栈溢出。
  
  即最后 `return` 的一定是函数本身就可以了。
  
* **对比语言**

    * **Swift**

      关于默认值，Swift 里也有。
      
      函数的 `length` 属性，我在 swift 里没有用到过，可能是参数传递没传过那么灵活吧，也就是 Rest 参数，我在 swift 里顶多就传个数组了；但是在灵活的 ES 里，这样用 `length` 判断可能挺有必要的吧。
      
      箭头函数这种新颖的函数表达方式，额，很容易让我联想到 Swift 的闭包，但是 JS 也有闭包，所以箭头函数只是函数的另一种表现形式罢了，不过好像 JS 的闭包也是函数形式的？
      
      `this` 确实是一个让人头疼的东西，涉猎虽浅，但已经有些云雾里了。Swift 里没有这样一个 `this`, 不也用的挺好的嘛。在我看来这个 `this` 就像一个语法糖样的东西，当然肯定不是语法糖能概括的，但是，搞得那么复杂，真的有必要吗？
      
      最后关于“尾递归”，这个在刚才学习的过程专门去搜索 Swift 里的尾递归，发现真的有这样的问题，其原理和 JS 的大概是一样的，所以在 Swift 开发里也要注意这个问题，避免复杂度过高。